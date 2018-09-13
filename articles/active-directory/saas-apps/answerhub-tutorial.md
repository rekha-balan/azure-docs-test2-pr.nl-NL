---
title: 'Tutorial: Azure Active Directory integration with AnswerHub | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and AnswerHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 818b91d7-01df-4b36-9706-f167c710a73c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 447a3911bc1f021fb1ca2658716de1910b5379b6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969167"
---
# <a name="tutorial-azure-active-directory-integration-with-answerhub"></a><span data-ttu-id="d8592-103">Tutorial: Azure Active Directory integration with AnswerHub</span><span class="sxs-lookup"><span data-stu-id="d8592-103">Tutorial: Azure Active Directory integration with AnswerHub</span></span>

<span data-ttu-id="d8592-104">In this tutorial, you learn how to integrate AnswerHub with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8592-104">In this tutorial, you learn how to integrate AnswerHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d8592-105">Integrating AnswerHub with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d8592-105">Integrating AnswerHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d8592-106">You can control in Azure AD who has access to AnswerHub</span><span class="sxs-lookup"><span data-stu-id="d8592-106">You can control in Azure AD who has access to AnswerHub</span></span>
- <span data-ttu-id="d8592-107">You can enable your users to automatically get signed-on to AnswerHub (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d8592-107">You can enable your users to automatically get signed-on to AnswerHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d8592-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d8592-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d8592-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d8592-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8592-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d8592-110">Prerequisites</span></span>

<span data-ttu-id="d8592-111">To configure Azure AD integration with AnswerHub, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d8592-111">To configure Azure AD integration with AnswerHub, you need the following items:</span></span>

- <span data-ttu-id="d8592-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d8592-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d8592-113">An AnswerHub single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d8592-113">An AnswerHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d8592-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d8592-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d8592-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d8592-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d8592-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d8592-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d8592-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8592-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d8592-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d8592-118">Scenario description</span></span>
<span data-ttu-id="d8592-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d8592-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d8592-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d8592-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d8592-121">Adding AnswerHub from the gallery</span><span class="sxs-lookup"><span data-stu-id="d8592-121">Adding AnswerHub from the gallery</span></span>
2. <span data-ttu-id="d8592-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d8592-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-answerhub-from-the-gallery"></a><span data-ttu-id="d8592-123">Adding AnswerHub from the gallery</span><span class="sxs-lookup"><span data-stu-id="d8592-123">Adding AnswerHub from the gallery</span></span>
<span data-ttu-id="d8592-124">To configure the integration of AnswerHub into Azure AD, you need to add AnswerHub from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d8592-124">To configure the integration of AnswerHub into Azure AD, you need to add AnswerHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d8592-125">**To add AnswerHub from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8592-125">**To add AnswerHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d8592-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d8592-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d8592-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d8592-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d8592-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d8592-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="d8592-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d8592-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="d8592-133">In the search box, type **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="d8592-133">In the search box, type **AnswerHub**.</span></span>

    ![Creating an Azure AD test user](./media/answerhub-tutorial/tutorial_answerhub_search.png)

5. <span data-ttu-id="d8592-135">In the results panel, select **AnswerHub**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d8592-135">In the results panel, select **AnswerHub**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/answerhub-tutorial/tutorial_answerhub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d8592-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d8592-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d8592-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d8592-138">In this section, you configure and test Azure AD single sign-on with AnswerHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d8592-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AnswerHub is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8592-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AnswerHub is to a user in Azure AD.</span></span> <span data-ttu-id="d8592-140">In other words, a link relationship between an Azure AD user and the related user in AnswerHub needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d8592-140">In other words, a link relationship between an Azure AD user and the related user in AnswerHub needs to be established.</span></span>

<span data-ttu-id="d8592-141">In AnswerHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="d8592-141">In AnswerHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d8592-142">To configure and test Azure AD single sign-on with AnswerHub, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d8592-142">To configure and test Azure AD single sign-on with AnswerHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d8592-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d8592-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d8592-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d8592-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d8592-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - to have a counterpart of Britta Simon in AnswerHub that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d8592-145">**[Creating an AnswerHub test user](#creating-an-answerhub-test-user)** - to have a counterpart of Britta Simon in AnswerHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d8592-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d8592-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d8592-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d8592-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d8592-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d8592-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d8592-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AnswerHub application.</span><span class="sxs-lookup"><span data-stu-id="d8592-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AnswerHub application.</span></span>

<span data-ttu-id="d8592-150">**To configure Azure AD single sign-on with AnswerHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8592-150">**To configure Azure AD single sign-on with AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="d8592-151">In the Azure portal, on the **AnswerHub** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d8592-151">In the Azure portal, on the **AnswerHub** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="d8592-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d8592-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/answerhub-tutorial/tutorial_answerhub_samlbase.png)

3. <span data-ttu-id="d8592-155">On the **AnswerHub Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8592-155">On the **AnswerHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/answerhub-tutorial/tutorial_answerhub_url.png)

    <span data-ttu-id="d8592-157">a.</span><span class="sxs-lookup"><span data-stu-id="d8592-157">a.</span></span> <span data-ttu-id="d8592-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="d8592-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    <span data-ttu-id="d8592-159">b.</span><span class="sxs-lookup"><span data-stu-id="d8592-159">b.</span></span> <span data-ttu-id="d8592-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span><span class="sxs-lookup"><span data-stu-id="d8592-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company>.answerhub.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d8592-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="d8592-161">These values are not real.</span></span> <span data-ttu-id="d8592-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="d8592-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d8592-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="d8592-163">Contact [AnswerHub Client support team](mailto:success@answerhub.com) to get these values.</span></span> 
 
4. <span data-ttu-id="d8592-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d8592-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/answerhub-tutorial/tutorial_answerhub_certificate.png) 

5. <span data-ttu-id="d8592-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d8592-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/answerhub-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d8592-168">On the **AnswerHub Configuration** section, click **Configure AnswerHub** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="d8592-168">On the **AnswerHub Configuration** section, click **Configure AnswerHub** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d8592-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="d8592-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/answerhub-tutorial/tutorial_answerhub_configure.png) 

7. <span data-ttu-id="d8592-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d8592-171">In a different web browser window, log into your AnswerHub company site as an administrator.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="d8592-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span><span class="sxs-lookup"><span data-stu-id="d8592-172">If you need help configuring AnswerHub, contact [AnswerHub's support team](mailto:success@answerhub.com.).</span></span>
   
8. <span data-ttu-id="d8592-173">Go to **Administration**.</span><span class="sxs-lookup"><span data-stu-id="d8592-173">Go to **Administration**.</span></span>

9. <span data-ttu-id="d8592-174">Click the **User and Group** tab.</span><span class="sxs-lookup"><span data-stu-id="d8592-174">Click the **User and Group** tab.</span></span>

10. <span data-ttu-id="d8592-175">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span><span class="sxs-lookup"><span data-stu-id="d8592-175">In the navigation pane on the left side, in the **Social Settings** section, click **SAML Setup**.</span></span>

11. <span data-ttu-id="d8592-176">Click **IDP Config** tab.</span><span class="sxs-lookup"><span data-stu-id="d8592-176">Click **IDP Config** tab.</span></span>

12. <span data-ttu-id="d8592-177">On the **IDP Config** tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8592-177">On the **IDP Config** tab, perform the following steps:</span></span>

     <span data-ttu-id="d8592-178">![SAML Setup](./media/answerhub-tutorial/ic785172.png "SAML Setup")</span><span class="sxs-lookup"><span data-stu-id="d8592-178">![SAML Setup](./media/answerhub-tutorial/ic785172.png "SAML Setup")</span></span>  
  
     <span data-ttu-id="d8592-179">a.</span><span class="sxs-lookup"><span data-stu-id="d8592-179">a.</span></span> <span data-ttu-id="d8592-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d8592-180">In **IDP Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
  
     <span data-ttu-id="d8592-181">b.</span><span class="sxs-lookup"><span data-stu-id="d8592-181">b.</span></span> <span data-ttu-id="d8592-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d8592-182">In **IDP Logout URL** textbox, paste **Sign-Out URL** value which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="d8592-183">c.</span><span class="sxs-lookup"><span data-stu-id="d8592-183">c.</span></span> <span data-ttu-id="d8592-184">In **IDP Name Identifier Format** textbox, enter the user Identifier value same as selected in Azure portal in **User Attributes** section.</span><span class="sxs-lookup"><span data-stu-id="d8592-184">In **IDP Name Identifier Format** textbox, enter the user Identifier value same as selected in Azure portal in **User Attributes** section.</span></span>
  
     <span data-ttu-id="d8592-185">d.</span><span class="sxs-lookup"><span data-stu-id="d8592-185">d.</span></span> <span data-ttu-id="d8592-186">Click **Keys and Certificates**.</span><span class="sxs-lookup"><span data-stu-id="d8592-186">Click **Keys and Certificates**.</span></span>

13. <span data-ttu-id="d8592-187">On the Keys and Certificates tab, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8592-187">On the Keys and Certificates tab, perform the following steps:</span></span>
    
     <span data-ttu-id="d8592-188">![Keys and Certificates](./media/answerhub-tutorial/ic785173.png "Keys and Certificates")</span><span class="sxs-lookup"><span data-stu-id="d8592-188">![Keys and Certificates](./media/answerhub-tutorial/ic785173.png "Keys and Certificates")</span></span>  
 
     <span data-ttu-id="d8592-189">a.</span><span class="sxs-lookup"><span data-stu-id="d8592-189">a.</span></span> <span data-ttu-id="d8592-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span><span class="sxs-lookup"><span data-stu-id="d8592-190">Open your base-64 encoded certificate which you have downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **IDP Public Key (x509 Format)** textbox.</span></span>
  
     <span data-ttu-id="d8592-191">b.</span><span class="sxs-lookup"><span data-stu-id="d8592-191">b.</span></span> <span data-ttu-id="d8592-192">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d8592-192">Click **Save**.</span></span>

14. <span data-ttu-id="d8592-193">On the **IDP Config** tab, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d8592-193">On the **IDP Config** tab, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d8592-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="d8592-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d8592-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d8592-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d8592-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d8592-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d8592-197">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d8592-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="d8592-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d8592-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="d8592-200">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8592-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d8592-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d8592-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/answerhub-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d8592-203">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d8592-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/answerhub-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d8592-205">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="d8592-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/answerhub-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d8592-207">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d8592-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/answerhub-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d8592-209">a.</span><span class="sxs-lookup"><span data-stu-id="d8592-209">a.</span></span> <span data-ttu-id="d8592-210">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d8592-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d8592-211">b.</span><span class="sxs-lookup"><span data-stu-id="d8592-211">b.</span></span> <span data-ttu-id="d8592-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d8592-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d8592-213">c.</span><span class="sxs-lookup"><span data-stu-id="d8592-213">c.</span></span> <span data-ttu-id="d8592-214">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="d8592-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d8592-215">d.</span><span class="sxs-lookup"><span data-stu-id="d8592-215">d.</span></span> <span data-ttu-id="d8592-216">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d8592-216">Click **Create**.</span></span>
 
### <a name="creating-an-answerhub-test-user"></a><span data-ttu-id="d8592-217">Creating an AnswerHub test user</span><span class="sxs-lookup"><span data-stu-id="d8592-217">Creating an AnswerHub test user</span></span>

<span data-ttu-id="d8592-218">To enable Azure AD users to log in to AnswerHub, they must be provisioned into AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="d8592-218">To enable Azure AD users to log in to AnswerHub, they must be provisioned into AnswerHub.</span></span>  
<span data-ttu-id="d8592-219">In the case of AnswerHub, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="d8592-219">In the case of AnswerHub, provisioning is a manual task.</span></span>

<span data-ttu-id="d8592-220">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8592-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d8592-221">Log in to your **AnswerHub** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="d8592-221">Log in to your **AnswerHub** company site as administrator.</span></span>

2. <span data-ttu-id="d8592-222">Go to **Administration**.</span><span class="sxs-lookup"><span data-stu-id="d8592-222">Go to **Administration**.</span></span>

3. <span data-ttu-id="d8592-223">Click the **Users & Groups** tab.</span><span class="sxs-lookup"><span data-stu-id="d8592-223">Click the **Users & Groups** tab.</span></span>

4. <span data-ttu-id="d8592-224">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span><span class="sxs-lookup"><span data-stu-id="d8592-224">In the navigation pane on the left side, in the **Manage Users** section, click **Create or import users**.</span></span>
   
   <span data-ttu-id="d8592-225">![Users & Groups](./media/answerhub-tutorial/ic785175.png "Users & Groups")</span><span class="sxs-lookup"><span data-stu-id="d8592-225">![Users & Groups](./media/answerhub-tutorial/ic785175.png "Users & Groups")</span></span>

5. <span data-ttu-id="d8592-226">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="d8592-226">Type the **Email address**, **Username** and **Password** of a valid Azure Active Directory account you want to provision into the related textboxes, and then click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="d8592-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="d8592-227">You can use any other AnswerHub user account creation tools or APIs provided by AnswerHub to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d8592-228">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d8592-228">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d8592-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AnswerHub.</span><span class="sxs-lookup"><span data-stu-id="d8592-229">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AnswerHub.</span></span>

![Assign User][200] 

<span data-ttu-id="d8592-231">**To assign Britta Simon to AnswerHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d8592-231">**To assign Britta Simon to AnswerHub, perform the following steps:**</span></span>

1. <span data-ttu-id="d8592-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d8592-232">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="d8592-234">In the applications list, select **AnswerHub**.</span><span class="sxs-lookup"><span data-stu-id="d8592-234">In the applications list, select **AnswerHub**.</span></span>

    ![Configure Single Sign-On](./media/answerhub-tutorial/tutorial_answerhub_app.png) 

3. <span data-ttu-id="d8592-236">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d8592-236">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="d8592-238">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d8592-238">Click **Add** button.</span></span> <span data-ttu-id="d8592-239">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d8592-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="d8592-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d8592-241">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d8592-242">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d8592-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d8592-243">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d8592-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d8592-244">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="d8592-244">Testing single sign-on</span></span>

<span data-ttu-id="d8592-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d8592-245">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d8592-246">When you click the AnswerHub tile in the Access Panel, you should get automatically signed-on to your AnswerHub application.</span><span class="sxs-lookup"><span data-stu-id="d8592-246">When you click the AnswerHub tile in the Access Panel, you should get automatically signed-on to your AnswerHub application.</span></span>
<span data-ttu-id="d8592-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d8592-247">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8592-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d8592-248">Additional resources</span></span>

* [<span data-ttu-id="d8592-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8592-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d8592-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d8592-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/answerhub-tutorial/tutorial_general_01.png
[2]: ./media/answerhub-tutorial/tutorial_general_02.png
[3]: ./media/answerhub-tutorial/tutorial_general_03.png
[4]: ./media/answerhub-tutorial/tutorial_general_04.png

[100]: ./media/answerhub-tutorial/tutorial_general_100.png

[200]: ./media/answerhub-tutorial/tutorial_general_200.png
[201]: ./media/answerhub-tutorial/tutorial_general_201.png
[202]: ./media/answerhub-tutorial/tutorial_general_202.png
[203]: ./media/answerhub-tutorial/tutorial_general_203.png

