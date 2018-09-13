---
title: 'Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Blackboard Learn - Shibboleth.
services: active-directory
documentationcenter: ''
author: jeevansd
manager: femila
editor: ''
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: cc674f12a668e017695bd0256c18c23d36b73b5e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556687"
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="f7e0a-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="f7e0a-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>
<span data-ttu-id="f7e0a-104">In this tutorial, you learn how to integrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f7e0a-104">In this tutorial, you learn how to integrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f7e0a-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f7e0a-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="f7e0a-106">You can control in Azure AD who has access to Blackboard Learn - Shibboleth</span><span class="sxs-lookup"><span data-stu-id="f7e0a-106">You can control in Azure AD who has access to Blackboard Learn - Shibboleth</span></span>
* <span data-ttu-id="f7e0a-107">You can enable your users to automatically get signed-on to Blackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f7e0a-107">You can enable your users to automatically get signed-on to Blackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="f7e0a-108">You can manage your accounts in one central location - the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="f7e0a-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="f7e0a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f7e0a-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7e0a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f7e0a-110">Prerequisites</span></span>
<span data-ttu-id="f7e0a-111">To configure Azure AD integration with Blackboard Learn - Shibboleth, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f7e0a-111">To configure Azure AD integration with Blackboard Learn - Shibboleth, you need the following items:</span></span>

* <span data-ttu-id="f7e0a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f7e0a-112">An Azure AD subscription</span></span>
* <span data-ttu-id="f7e0a-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f7e0a-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f7e0a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="f7e0a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f7e0a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="f7e0a-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="f7e0a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7e0a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f7e0a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f7e0a-118">Scenario description</span></span>
<span data-ttu-id="f7e0a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="f7e0a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f7e0a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f7e0a-121">Adding Blackboard Learn - Shibboleth from the gallery</span><span class="sxs-lookup"><span data-stu-id="f7e0a-121">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
2. <span data-ttu-id="f7e0a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f7e0a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-the-gallery"></a><span data-ttu-id="f7e0a-123">Adding Blackboard Learn - Shibboleth from the gallery</span><span class="sxs-lookup"><span data-stu-id="f7e0a-123">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
<span data-ttu-id="f7e0a-124">To configure the integration of Blackboard Learn - Shibboleth into Azure AD, you need to add Blackboard Learn - Shibboleth from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-124">To configure the integration of Blackboard Learn - Shibboleth into Azure AD, you need to add Blackboard Learn - Shibboleth from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f7e0a-125">**To add Blackboard Learn - Shibboleth from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f7e0a-125">**To add Blackboard Learn - Shibboleth from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e0a-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Active Directory][1]

2. <span data-ttu-id="f7e0a-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f7e0a-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Applications][2]

4. <span data-ttu-id="f7e0a-131">Click **Add** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Applications][3]

5. <span data-ttu-id="f7e0a-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Applications][4]

6. <span data-ttu-id="f7e0a-135">In the search box, type **Blackboard Learn - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-135">In the search box, type **Blackboard Learn - Shibboleth**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearnshibboleth_01.png)

7. <span data-ttu-id="f7e0a-137">In the results pane, select **Blackboard Learn - Shibboleth**, and then click **Complete** to add the application.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-137">In the results pane, select **Blackboard Learn - Shibboleth**, and then click **Complete** to add the application.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearnshibboleth_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f7e0a-139">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f7e0a-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f7e0a-140">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f7e0a-140">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f7e0a-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn - Shibboleth is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn - Shibboleth is to a user in Azure AD.</span></span> <span data-ttu-id="f7e0a-142">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn - Shibboleth needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-142">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn - Shibboleth needs to be established.</span></span>

<span data-ttu-id="f7e0a-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Blackboard Learn - Shibboleth.</span></span>

<span data-ttu-id="f7e0a-144">To configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f7e0a-144">To configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f7e0a-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f7e0a-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f7e0a-147">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn-shibboleth-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-147">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn-shibboleth-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="f7e0a-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f7e0a-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f7e0a-150">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f7e0a-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="f7e0a-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="f7e0a-152">**To configure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f7e0a-152">**To configure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e0a-153">In the classic portal, on the **Blackboard Learn - Shibboleth** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-153">In the classic portal, on the **Blackboard Learn - Shibboleth** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Configure Single Sign-On][6] 

2. <span data-ttu-id="f7e0a-155">On the **How would you like users to sign on to Blackboard Learn - Shibboleth** page, select **Azure AD Single Sign-On**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-155">On the **How would you like users to sign on to Blackboard Learn - Shibboleth** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearnshibboleth_03.png) 

3. <span data-ttu-id="f7e0a-157">On the **Configure App Settings** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f7e0a-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearnshibboleth_04.png) 
   
    <span data-ttu-id="f7e0a-159">a.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-159">a.</span></span> <span data-ttu-id="f7e0a-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Blackboard Learn - Shibboleth application using the following pattern: **https://\<yourblackoardlearnserver\>.blackboardlearn.com/Shibboleth.sso/Login**</span><span class="sxs-lookup"><span data-stu-id="f7e0a-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Blackboard Learn - Shibboleth application using the following pattern: **https://\<yourblackoardlearnserver\>.blackboardlearn.com/Shibboleth.sso/Login**</span></span>
   
    <span data-ttu-id="f7e0a-161">b.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-161">b.</span></span> <span data-ttu-id="f7e0a-162">In the **Identifier** textbox, type the URL using the following pattern: **https://\<yourblackoardlearnserver\>.blackboardlearn.com/shibboleth-sp**</span><span class="sxs-lookup"><span data-stu-id="f7e0a-162">In the **Identifier** textbox, type the URL using the following pattern: **https://\<yourblackoardlearnserver\>.blackboardlearn.com/shibboleth-sp**</span></span>
   
    <span data-ttu-id="f7e0a-163">c.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-163">c.</span></span> <span data-ttu-id="f7e0a-164">In the **Reply URL** textbox, type the URL using the following pattern: **https://\<yourblackoardlearnserver\>.blackboardlearn.com/Shibboleth.sso/SAML2/POST**</span><span class="sxs-lookup"><span data-stu-id="f7e0a-164">In the **Reply URL** textbox, type the URL using the following pattern: **https://\<yourblackoardlearnserver\>.blackboardlearn.com/Shibboleth.sso/SAML2/POST**</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="f7e0a-165">You will able to find all these values in the Federation Metadata doucument provided by your Blackboard Learn partner.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-165">You will able to find all these values in the Federation Metadata doucument provided by your Blackboard Learn partner.</span></span>
    > 
    > 
   
    <span data-ttu-id="f7e0a-166">d.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-166">d.</span></span> <span data-ttu-id="f7e0a-167">click **Next**</span><span class="sxs-lookup"><span data-stu-id="f7e0a-167">click **Next**</span></span>

4. <span data-ttu-id="f7e0a-168">On the **Configure single sign-on at Blackboard Learn - Shibboleth** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f7e0a-168">On the **Configure single sign-on at Blackboard Learn - Shibboleth** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearnshibboleth_05.png)
   
    <span data-ttu-id="f7e0a-170">a.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-170">a.</span></span> <span data-ttu-id="f7e0a-171">Click **Download metadata**, and then save the file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-171">Click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="f7e0a-172">b.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-172">b.</span></span> <span data-ttu-id="f7e0a-173">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-173">Click **Next**.</span></span>

5. <span data-ttu-id="f7e0a-174">To get SSO configured for your application, contact your Blackboard Learn - Shibboleth partner and provide them with the following:</span><span class="sxs-lookup"><span data-stu-id="f7e0a-174">To get SSO configured for your application, contact your Blackboard Learn - Shibboleth partner and provide them with the following:</span></span>
   
    <span data-ttu-id="f7e0a-175">• The downloaded **metadata**</span><span class="sxs-lookup"><span data-stu-id="f7e0a-175">• The downloaded **metadata**</span></span>
   
    <span data-ttu-id="f7e0a-176">• The **Issuer URL**</span><span class="sxs-lookup"><span data-stu-id="f7e0a-176">• The **Issuer URL**</span></span>
   
    <span data-ttu-id="f7e0a-177">• The **SAML SSO URL**</span><span class="sxs-lookup"><span data-stu-id="f7e0a-177">• The **SAML SSO URL**</span></span>
   
    <span data-ttu-id="f7e0a-178">• The **Single Sign-out service URL**</span><span class="sxs-lookup"><span data-stu-id="f7e0a-178">• The **Single Sign-out service URL**</span></span>

6. <span data-ttu-id="f7e0a-179">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-179">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD Single Sign-On][10]

7. <span data-ttu-id="f7e0a-181">On the **Single sign-on confirmation** page, click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-181">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD Single Sign-On][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f7e0a-183">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f7e0a-183">Creating an Azure AD test user</span></span>
<span data-ttu-id="f7e0a-184">In this section, you create a test user in the classic portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-184">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Create Azure AD User][20]

<span data-ttu-id="f7e0a-186">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f7e0a-186">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e0a-187">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-187">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="f7e0a-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-189">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="f7e0a-190">To display the list of users, in the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-190">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f7e0a-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-192">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="f7e0a-194">On the **Tell us about this user** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f7e0a-194">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="f7e0a-196">a.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-196">a.</span></span> <span data-ttu-id="f7e0a-197">As Type Of User, select New user in your organization.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-197">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="f7e0a-198">b.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-198">b.</span></span> <span data-ttu-id="f7e0a-199">In the User Name **textbox**, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-199">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="f7e0a-200">c.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-200">c.</span></span> <span data-ttu-id="f7e0a-201">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-201">Click **Next**.</span></span>

6. <span data-ttu-id="f7e0a-202">On the **User Profile** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_06.png)</span><span class="sxs-lookup"><span data-stu-id="f7e0a-202">On the **User Profile** dialog page, perform the following steps:  ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_06.png)</span></span> 
   
    <span data-ttu-id="f7e0a-203">a.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-203">a.</span></span> <span data-ttu-id="f7e0a-204">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-204">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="f7e0a-205">b.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-205">b.</span></span> <span data-ttu-id="f7e0a-206">In the **Last Name** textbox, type, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-206">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="f7e0a-207">c.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-207">c.</span></span> <span data-ttu-id="f7e0a-208">In the **Display Name** textbox, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-208">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="f7e0a-209">d.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-209">d.</span></span> <span data-ttu-id="f7e0a-210">In the **Role** list, select **User**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-210">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="f7e0a-211">e.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-211">e.</span></span> <span data-ttu-id="f7e0a-212">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-212">Click **Next**.</span></span>

7. <span data-ttu-id="f7e0a-213">On the **Get temporary password** dialog page, click **create**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-213">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="f7e0a-215">On the **Get temporary password** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f7e0a-215">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="f7e0a-217">a.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-217">a.</span></span> <span data-ttu-id="f7e0a-218">Write down the value of the **New Password**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-218">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="f7e0a-219">b.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-219">b.</span></span> <span data-ttu-id="f7e0a-220">Click **Complete**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-220">Click **Complete**.</span></span>   

### <a name="creating-an-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="f7e0a-221">Creating an Blackboard Learn - Shibboleth test user</span><span class="sxs-lookup"><span data-stu-id="f7e0a-221">Creating an Blackboard Learn - Shibboleth test user</span></span>
<span data-ttu-id="f7e0a-222">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-222">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="f7e0a-223">Please work with your Blackboard Learn partner to add the users in the Blackboard Learn - Shibboleth platform.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-223">Please work with your Blackboard Learn partner to add the users in the Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f7e0a-224">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f7e0a-224">Assigning the Azure AD test user</span></span>
<span data-ttu-id="f7e0a-225">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Blackboard Learn - Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-225">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Blackboard Learn - Shibboleth.</span></span>

![Assign User][200] 

<span data-ttu-id="f7e0a-227">**To assign Britta Simon to Blackboard Learn - Shibboleth, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f7e0a-227">**To assign Britta Simon to Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="f7e0a-228">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-228">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Assign User][201] 

2. <span data-ttu-id="f7e0a-230">In the applications list, select **Blackboard Learn - Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-230">In the applications list, select **Blackboard Learn - Shibboleth**.</span></span>
   
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearnshibboleth_50.png) 

3. <span data-ttu-id="f7e0a-232">In the menu on the top, click **Users**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-232">In the menu on the top, click **Users**.</span></span>
   
    ![Assign User][203]

4. <span data-ttu-id="f7e0a-234">In the Users list, select **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-234">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="f7e0a-235">In the toolbar on the bottom, click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-235">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Assign User][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="f7e0a-237">Testing Single Sign-On</span><span class="sxs-lookup"><span data-stu-id="f7e0a-237">Testing Single Sign-On</span></span>
<span data-ttu-id="f7e0a-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-238">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f7e0a-239">When you click the Blackboard Learn - Shibboleth tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn - Shibboleth application.</span><span class="sxs-lookup"><span data-stu-id="f7e0a-239">When you click the Blackboard Learn - Shibboleth tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f7e0a-240">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f7e0a-240">Additional resources</span></span>
* [<span data-ttu-id="f7e0a-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f7e0a-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f7e0a-242">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f7e0a-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_05.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_06.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_07.png
[20]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_204.png
[205]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_205.png

























