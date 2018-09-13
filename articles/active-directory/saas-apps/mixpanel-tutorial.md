---
title: 'Tutorial: Azure Active Directory integration with Mixpanel | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Mixpanel.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: a2df26ef-d441-44ac-a9f3-b37bf9709bcb
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 9ec0b27defdc4c859415e78e1cb6e43f5ed0b208
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869212"
---
# <a name="tutorial-azure-active-directory-integration-with-mixpanel"></a><span data-ttu-id="504a9-103">Tutorial: Azure Active Directory integration with Mixpanel</span><span class="sxs-lookup"><span data-stu-id="504a9-103">Tutorial: Azure Active Directory integration with Mixpanel</span></span>

<span data-ttu-id="504a9-104">In this tutorial, you learn how to integrate Mixpanel with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="504a9-104">In this tutorial, you learn how to integrate Mixpanel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="504a9-105">Integrating Mixpanel with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="504a9-105">Integrating Mixpanel with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="504a9-106">You can control in Azure AD who has access to Mixpanel</span><span class="sxs-lookup"><span data-stu-id="504a9-106">You can control in Azure AD who has access to Mixpanel</span></span>
- <span data-ttu-id="504a9-107">You can enable your users to automatically get signed-on to Mixpanel (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="504a9-107">You can enable your users to automatically get signed-on to Mixpanel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="504a9-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="504a9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="504a9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="504a9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="504a9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="504a9-110">Prerequisites</span></span>

<span data-ttu-id="504a9-111">To configure Azure AD integration with Mixpanel, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="504a9-111">To configure Azure AD integration with Mixpanel, you need the following items:</span></span>

- <span data-ttu-id="504a9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="504a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="504a9-113">A Mixpanel single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="504a9-113">A Mixpanel single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="504a9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="504a9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="504a9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="504a9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="504a9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="504a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="504a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="504a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="504a9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="504a9-118">Scenario description</span></span>
<span data-ttu-id="504a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="504a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="504a9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="504a9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="504a9-121">Adding Mixpanel from the gallery</span><span class="sxs-lookup"><span data-stu-id="504a9-121">Adding Mixpanel from the gallery</span></span>
1. <span data-ttu-id="504a9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="504a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mixpanel-from-the-gallery"></a><span data-ttu-id="504a9-123">Adding Mixpanel from the gallery</span><span class="sxs-lookup"><span data-stu-id="504a9-123">Adding Mixpanel from the gallery</span></span>
<span data-ttu-id="504a9-124">To configure the integration of Mixpanel into Azure AD, you need to add Mixpanel from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="504a9-124">To configure the integration of Mixpanel into Azure AD, you need to add Mixpanel from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="504a9-125">**To add Mixpanel from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="504a9-125">**To add Mixpanel from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="504a9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="504a9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="504a9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="504a9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="504a9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="504a9-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="504a9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="504a9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="504a9-133">In the search box, type **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="504a9-133">In the search box, type **Mixpanel**.</span></span>

    ![Creating an Azure AD test user](./media/mixpanel-tutorial/tutorial_mixpanel_search.png)

1. <span data-ttu-id="504a9-135">In the results panel, select **Mixpanel**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="504a9-135">In the results panel, select **Mixpanel**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/mixpanel-tutorial/tutorial_mixpanel_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="504a9-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="504a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="504a9-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="504a9-138">In this section, you configure and test Azure AD single sign-on with Mixpanel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="504a9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mixpanel is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="504a9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mixpanel is to a user in Azure AD.</span></span> <span data-ttu-id="504a9-140">In other words, a link relationship between an Azure AD user and the related user in Mixpanel needs to be established.</span><span class="sxs-lookup"><span data-stu-id="504a9-140">In other words, a link relationship between an Azure AD user and the related user in Mixpanel needs to be established.</span></span>

<span data-ttu-id="504a9-141">In Mixpanel, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="504a9-141">In Mixpanel, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="504a9-142">To configure and test Azure AD single sign-on with Mixpanel, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="504a9-142">To configure and test Azure AD single sign-on with Mixpanel, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="504a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="504a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="504a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="504a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="504a9-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - to have a counterpart of Britta Simon in Mixpanel that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="504a9-145">**[Creating a Mixpanel test user](#creating-a-mixpanel-test-user)** - to have a counterpart of Britta Simon in Mixpanel that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="504a9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="504a9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="504a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="504a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="504a9-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="504a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="504a9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mixpanel application.</span><span class="sxs-lookup"><span data-stu-id="504a9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mixpanel application.</span></span>

<span data-ttu-id="504a9-150">**To configure Azure AD single sign-on with Mixpanel, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="504a9-150">**To configure Azure AD single sign-on with Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="504a9-151">In the Azure portal, on the **Mixpanel** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="504a9-151">In the Azure portal, on the **Mixpanel** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="504a9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="504a9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/mixpanel-tutorial/tutorial_mixpanel_samlbase.png)

1. <span data-ttu-id="504a9-155">On the **Mixpanel Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="504a9-155">On the **Mixpanel Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/mixpanel-tutorial/tutorial_mixpanel_url.png)

     <span data-ttu-id="504a9-157">In the **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span><span class="sxs-lookup"><span data-stu-id="504a9-157">In the **Sign-on URL** textbox, type a URL as: `https://mixpanel.com/login/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="504a9-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) to set up your login credentials and  contact the [Mixpanel support team](mailto:support@mixpanel.com) to enable SSO settings for your tenant.</span><span class="sxs-lookup"><span data-stu-id="504a9-158">Please register at [https://mixpanel.com/register/](https://mixpanel.com/register/) to set up your login credentials and  contact the [Mixpanel support team](mailto:support@mixpanel.com) to enable SSO settings for your tenant.</span></span> <span data-ttu-id="504a9-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span><span class="sxs-lookup"><span data-stu-id="504a9-159">You can also get your Sign On URL value if necessary from your Mixpanel support team.</span></span> 
 
1. <span data-ttu-id="504a9-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="504a9-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/mixpanel-tutorial/tutorial_mixpanel_certificate.png) 

1. <span data-ttu-id="504a9-162">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="504a9-162">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/mixpanel-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="504a9-164">On the **Mixpanel Configuration** section, click **Configure Mixpanel** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="504a9-164">On the **Mixpanel Configuration** section, click **Configure Mixpanel** to open **Configure sign-on** window.</span></span> <span data-ttu-id="504a9-165">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="504a9-165">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/mixpanel-tutorial/tutorial_mixpanel_configure.png) 

1. <span data-ttu-id="504a9-167">In a different browser window, sign-on to your Mixpanel application as an administrator.</span><span class="sxs-lookup"><span data-stu-id="504a9-167">In a different browser window, sign-on to your Mixpanel application as an administrator.</span></span>

1. <span data-ttu-id="504a9-168">On bottom of the page, click the little **gear** icon in the left corner.</span><span class="sxs-lookup"><span data-stu-id="504a9-168">On bottom of the page, click the little **gear** icon in the left corner.</span></span> 
   
    ![Mixpanel Single Sign-On](./media/mixpanel-tutorial/tutorial_mixpanel_06.png) 

1. <span data-ttu-id="504a9-170">Click the **Access security** tab, and then click **Change settings**.</span><span class="sxs-lookup"><span data-stu-id="504a9-170">Click the **Access security** tab, and then click **Change settings**.</span></span>
   
    ![Mixpanel Settings](./media/mixpanel-tutorial/tutorial_mixpanel_08.png) 

1. <span data-ttu-id="504a9-172">On the **Change your certificate** dialog page, click **Choose file** to upload your downloaded certificate, and then click **NEXT**.</span><span class="sxs-lookup"><span data-stu-id="504a9-172">On the **Change your certificate** dialog page, click **Choose file** to upload your downloaded certificate, and then click **NEXT**.</span></span>
   
    ![Mixpanel Settings](./media/mixpanel-tutorial/tutorial_mixpanel_09.png) 

1.  <span data-ttu-id="504a9-174">In the authentication URL textbox on the **Change your authentication  URL** dialog page, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span><span class="sxs-lookup"><span data-stu-id="504a9-174">In the authentication URL textbox on the **Change your authentication  URL** dialog page, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal, and then click **NEXT**.</span></span>
   
   ![Mixpanel Settings](./media/mixpanel-tutorial/tutorial_mixpanel_10.png) 

1. <span data-ttu-id="504a9-176">Click **Done**.</span><span class="sxs-lookup"><span data-stu-id="504a9-176">Click **Done**.</span></span>

> [!TIP]
> <span data-ttu-id="504a9-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="504a9-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="504a9-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="504a9-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="504a9-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="504a9-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="504a9-180">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="504a9-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="504a9-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="504a9-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="504a9-183">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="504a9-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="504a9-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="504a9-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/mixpanel-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="504a9-186">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="504a9-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/mixpanel-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="504a9-188">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="504a9-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/mixpanel-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="504a9-190">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="504a9-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/mixpanel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="504a9-192">a.</span><span class="sxs-lookup"><span data-stu-id="504a9-192">a.</span></span> <span data-ttu-id="504a9-193">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="504a9-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="504a9-194">b.</span><span class="sxs-lookup"><span data-stu-id="504a9-194">b.</span></span> <span data-ttu-id="504a9-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="504a9-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="504a9-196">c.</span><span class="sxs-lookup"><span data-stu-id="504a9-196">c.</span></span> <span data-ttu-id="504a9-197">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="504a9-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="504a9-198">d.</span><span class="sxs-lookup"><span data-stu-id="504a9-198">d.</span></span> <span data-ttu-id="504a9-199">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="504a9-199">Click **Create**.</span></span>
 
### <a name="creating-a-mixpanel-test-user"></a><span data-ttu-id="504a9-200">Creating a Mixpanel test user</span><span class="sxs-lookup"><span data-stu-id="504a9-200">Creating a Mixpanel test user</span></span>

<span data-ttu-id="504a9-201">The objective of this section is to create a user called Britta Simon in Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="504a9-201">The objective of this section is to create a user called Britta Simon in Mixpanel.</span></span> 

1. <span data-ttu-id="504a9-202">Sign on to your Mixpanel company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="504a9-202">Sign on to your Mixpanel company site as an administrator.</span></span>

1. <span data-ttu-id="504a9-203">On the bottom of the page, click the little gear button on the left corner to open the **Settings** window.</span><span class="sxs-lookup"><span data-stu-id="504a9-203">On the bottom of the page, click the little gear button on the left corner to open the **Settings** window.</span></span>

1. <span data-ttu-id="504a9-204">Click the **Team** tab.</span><span class="sxs-lookup"><span data-stu-id="504a9-204">Click the **Team** tab.</span></span>

1. <span data-ttu-id="504a9-205">In the **team member** textbox, type Britta's email address in the Azure.</span><span class="sxs-lookup"><span data-stu-id="504a9-205">In the **team member** textbox, type Britta's email address in the Azure.</span></span>
   
    ![Mixpanel Settings](./media/mixpanel-tutorial/tutorial_mixpanel_11.png) 

1. <span data-ttu-id="504a9-207">Click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="504a9-207">Click **Invite**.</span></span> 

> [!Note]
> <span data-ttu-id="504a9-208">The user will get an email to set up the profile.</span><span class="sxs-lookup"><span data-stu-id="504a9-208">The user will get an email to set up the profile.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="504a9-209">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="504a9-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="504a9-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mixpanel.</span><span class="sxs-lookup"><span data-stu-id="504a9-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mixpanel.</span></span>

![Assign User][200] 

<span data-ttu-id="504a9-212">**To assign Britta Simon to Mixpanel, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="504a9-212">**To assign Britta Simon to Mixpanel, perform the following steps:**</span></span>

1. <span data-ttu-id="504a9-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="504a9-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="504a9-215">In the applications list, select **Mixpanel**.</span><span class="sxs-lookup"><span data-stu-id="504a9-215">In the applications list, select **Mixpanel**.</span></span>

    ![Configure Single Sign-On](./media/mixpanel-tutorial/tutorial_mixpanel_app.png) 

1. <span data-ttu-id="504a9-217">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="504a9-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="504a9-219">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="504a9-219">Click **Add** button.</span></span> <span data-ttu-id="504a9-220">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="504a9-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="504a9-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="504a9-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="504a9-223">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="504a9-223">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="504a9-224">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="504a9-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="504a9-225">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="504a9-225">Testing single sign-on</span></span>

<span data-ttu-id="504a9-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="504a9-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="504a9-227">When you click the Mixpanel tile in the Access Panel, you should get automatically signed-on to your Mixpanel application.</span><span class="sxs-lookup"><span data-stu-id="504a9-227">When you click the Mixpanel tile in the Access Panel, you should get automatically signed-on to your Mixpanel application.</span></span>
<span data-ttu-id="504a9-228">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="504a9-228">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="504a9-229">Additional resources</span><span class="sxs-lookup"><span data-stu-id="504a9-229">Additional resources</span></span>

* [<span data-ttu-id="504a9-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="504a9-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="504a9-231">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="504a9-231">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/mixpanel-tutorial/tutorial_general_01.png
[2]: ./media/mixpanel-tutorial/tutorial_general_02.png
[3]: ./media/mixpanel-tutorial/tutorial_general_03.png
[4]: ./media/mixpanel-tutorial/tutorial_general_04.png

[100]: ./media/mixpanel-tutorial/tutorial_general_100.png

[200]: ./media/mixpanel-tutorial/tutorial_general_200.png
[201]: ./media/mixpanel-tutorial/tutorial_general_201.png
[202]: ./media/mixpanel-tutorial/tutorial_general_202.png
[203]: ./media/mixpanel-tutorial/tutorial_general_203.png

