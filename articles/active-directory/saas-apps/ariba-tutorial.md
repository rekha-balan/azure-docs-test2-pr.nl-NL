---
title: 'Tutorial: Azure Active Directory integration with Ariba | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Ariba.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: d0bf000bc4f921a1f594aab9e0d54edb30f88963
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855785"
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="2d6ac-103">Tutorial: Azure Active Directory integration with Ariba</span><span class="sxs-lookup"><span data-stu-id="2d6ac-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="2d6ac-104">In this tutorial, you learn how to integrate Ariba with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2d6ac-104">In this tutorial, you learn how to integrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2d6ac-105">Integrating Ariba with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2d6ac-105">Integrating Ariba with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2d6ac-106">You can control in Azure AD who has access to Ariba</span><span class="sxs-lookup"><span data-stu-id="2d6ac-106">You can control in Azure AD who has access to Ariba</span></span>
- <span data-ttu-id="2d6ac-107">You can enable your users to automatically get signed-on to Ariba (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="2d6ac-107">You can enable your users to automatically get signed-on to Ariba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2d6ac-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2d6ac-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2d6ac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="2d6ac-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2d6ac-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2d6ac-110">Prerequisites</span></span>

<span data-ttu-id="2d6ac-111">To configure Azure AD integration with Ariba, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2d6ac-111">To configure Azure AD integration with Ariba, you need the following items:</span></span>

- <span data-ttu-id="2d6ac-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2d6ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2d6ac-113">An Ariba single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2d6ac-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2d6ac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2d6ac-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2d6ac-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2d6ac-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2d6ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2d6ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2d6ac-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2d6ac-118">Scenario description</span></span>
<span data-ttu-id="2d6ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2d6ac-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2d6ac-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2d6ac-121">Adding Ariba from the gallery</span><span class="sxs-lookup"><span data-stu-id="2d6ac-121">Adding Ariba from the gallery</span></span>
1. <span data-ttu-id="2d6ac-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2d6ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-the-gallery"></a><span data-ttu-id="2d6ac-123">Adding Ariba from the gallery</span><span class="sxs-lookup"><span data-stu-id="2d6ac-123">Adding Ariba from the gallery</span></span>
<span data-ttu-id="2d6ac-124">To configure the integration of Ariba into Azure AD, you need to add Ariba from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-124">To configure the integration of Ariba into Azure AD, you need to add Ariba from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2d6ac-125">**To add Ariba from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2d6ac-125">**To add Ariba from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2d6ac-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="2d6ac-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2d6ac-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="2d6ac-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="2d6ac-133">In the search box, type **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-133">In the search box, type **Ariba**.</span></span>

    ![Creating an Azure AD test user](./media/ariba-tutorial/tutorial_ariba_search.png)

1. <span data-ttu-id="2d6ac-135">In the results panel, select **Ariba**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-135">In the results panel, select **Ariba**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2d6ac-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2d6ac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2d6ac-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2d6ac-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2d6ac-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Ariba is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Ariba is to a user in Azure AD.</span></span> <span data-ttu-id="2d6ac-140">In other words, a link relationship between an Azure AD user and the related user in Ariba needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-140">In other words, a link relationship between an Azure AD user and the related user in Ariba needs to be established.</span></span>

<span data-ttu-id="2d6ac-141">In Ariba, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-141">In Ariba, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="2d6ac-142">To configure and test Azure AD single sign-on with Ariba, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2d6ac-142">To configure and test Azure AD single sign-on with Ariba, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2d6ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="2d6ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="2d6ac-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - to have a counterpart of Britta Simon in Ariba that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - to have a counterpart of Britta Simon in Ariba that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="2d6ac-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="2d6ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2d6ac-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2d6ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2d6ac-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ariba application.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="2d6ac-150">**To configure Azure AD single sign-on with Ariba, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2d6ac-150">**To configure Azure AD single sign-on with Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="2d6ac-151">In the Azure portal, on the **Ariba** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-151">In the Azure portal, on the **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="2d6ac-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/ariba-tutorial/tutorial_ariba_samlbase.png)

1. <span data-ttu-id="2d6ac-155">On the **Ariba Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2d6ac-155">On the **Ariba Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="2d6ac-157">a.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-157">a.</span></span> <span data-ttu-id="2d6ac-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="2d6ac-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="2d6ac-159">b.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-159">b.</span></span> <span data-ttu-id="2d6ac-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="2d6ac-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="2d6ac-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-161">These values are not real.</span></span> <span data-ttu-id="2d6ac-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2d6ac-163">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="2d6ac-164">Contact Ariba Client support team at **1-866-218-2155** to get these values.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-164">Contact Ariba Client support team at **1-866-218-2155** to get these values.</span></span> 
 

1. <span data-ttu-id="2d6ac-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate  file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate  file on your computer.</span></span>

    ![Configure Single Sign-On](./media/ariba-tutorial/tutorial_ariba_certificate.png) 

1. <span data-ttu-id="2d6ac-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/ariba-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="2d6ac-169">To get SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how to provide them the downloaded **Certificate (Base64)** file.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-169">To get SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how to provide them the downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="2d6ac-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="2d6ac-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2d6ac-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2d6ac-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2d6ac-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2d6ac-173">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2d6ac-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="2d6ac-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="2d6ac-176">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2d6ac-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2d6ac-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/ariba-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="2d6ac-179">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/ariba-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="2d6ac-181">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/ariba-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="2d6ac-183">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2d6ac-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2d6ac-185">a.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-185">a.</span></span> <span data-ttu-id="2d6ac-186">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2d6ac-187">b.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-187">b.</span></span> <span data-ttu-id="2d6ac-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2d6ac-189">c.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-189">c.</span></span> <span data-ttu-id="2d6ac-190">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2d6ac-191">d.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-191">d.</span></span> <span data-ttu-id="2d6ac-192">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="2d6ac-193">Creating an Ariba test user</span><span class="sxs-lookup"><span data-stu-id="2d6ac-193">Creating an Ariba test user</span></span>

<span data-ttu-id="2d6ac-194">The objective of this section is to create a user called Britta Simon in Ariba.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-194">The objective of this section is to create a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="2d6ac-195">Work with Ariba support team at **1-866-218-2155** to add the users in the Ariba system.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-195">Work with Ariba support team at **1-866-218-2155** to add the users in the Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="2d6ac-196">If you need to create a user manually, you need to contact the Ariba support team at **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-196">If you need to create a user manually, you need to contact the Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2d6ac-197">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2d6ac-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2d6ac-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ariba.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ariba.</span></span>

![Assign User][200] 

<span data-ttu-id="2d6ac-200">**To assign Britta Simon to Ariba, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2d6ac-200">**To assign Britta Simon to Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="2d6ac-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="2d6ac-203">In the applications list, select **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-203">In the applications list, select **Ariba**.</span></span>

    ![Configure Single Sign-On](./media/ariba-tutorial/tutorial_ariba_app.png) 

1. <span data-ttu-id="2d6ac-205">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="2d6ac-207">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-207">Click **Add** button.</span></span> <span data-ttu-id="2d6ac-208">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="2d6ac-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="2d6ac-211">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-211">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="2d6ac-212">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2d6ac-213">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="2d6ac-213">Testing single sign-on</span></span>
<span data-ttu-id="2d6ac-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="2d6ac-215">When you click the Ariba tile in the Access Panel, you should get automatically signed-on to your Ariba application.</span><span class="sxs-lookup"><span data-stu-id="2d6ac-215">When you click the Ariba tile in the Access Panel, you should get automatically signed-on to your Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2d6ac-216">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2d6ac-216">Additional resources</span></span>

* [<span data-ttu-id="2d6ac-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2d6ac-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="2d6ac-218">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2d6ac-218">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/ariba-tutorial/tutorial_general_01.png
[2]: ./media/ariba-tutorial/tutorial_general_02.png
[3]: ./media/ariba-tutorial/tutorial_general_03.png
[4]: ./media/ariba-tutorial/tutorial_general_04.png

[100]: ./media/ariba-tutorial/tutorial_general_100.png

[200]: ./media/ariba-tutorial/tutorial_general_200.png
[201]: ./media/ariba-tutorial/tutorial_general_201.png
[202]: ./media/ariba-tutorial/tutorial_general_202.png
[203]: ./media/ariba-tutorial/tutorial_general_203.png
