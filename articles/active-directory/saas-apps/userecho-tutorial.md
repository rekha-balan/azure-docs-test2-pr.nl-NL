---
title: 'Tutorial: Azure Active Directory integration with UserEcho | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and UserEcho.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: bedd916b-8f69-4b50-9b8d-56f4ee3bd3ed
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: ecdd37db662c6861e35f80bfbf4ac8ff7e0d08c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868220"
---
# <a name="tutorial-azure-active-directory-integration-with-userecho"></a><span data-ttu-id="0e11a-103">Tutorial: Azure Active Directory integration with UserEcho</span><span class="sxs-lookup"><span data-stu-id="0e11a-103">Tutorial: Azure Active Directory integration with UserEcho</span></span>

<span data-ttu-id="0e11a-104">In this tutorial, you learn how to integrate UserEcho with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0e11a-104">In this tutorial, you learn how to integrate UserEcho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0e11a-105">Integrating UserEcho with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="0e11a-105">Integrating UserEcho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0e11a-106">You can control in Azure AD who has access to UserEcho</span><span class="sxs-lookup"><span data-stu-id="0e11a-106">You can control in Azure AD who has access to UserEcho</span></span>
- <span data-ttu-id="0e11a-107">You can enable your users to automatically get signed-on to UserEcho (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="0e11a-107">You can enable your users to automatically get signed-on to UserEcho (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0e11a-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0e11a-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0e11a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="0e11a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e11a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0e11a-110">Prerequisites</span></span>

<span data-ttu-id="0e11a-111">To configure Azure AD integration with UserEcho, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0e11a-111">To configure Azure AD integration with UserEcho, you need the following items:</span></span>

- <span data-ttu-id="0e11a-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0e11a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0e11a-113">A UserEcho single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0e11a-113">A UserEcho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0e11a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0e11a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0e11a-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0e11a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0e11a-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0e11a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0e11a-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e11a-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0e11a-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="0e11a-118">Scenario description</span></span>
<span data-ttu-id="0e11a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="0e11a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0e11a-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="0e11a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0e11a-121">Adding UserEcho from the gallery</span><span class="sxs-lookup"><span data-stu-id="0e11a-121">Adding UserEcho from the gallery</span></span>
1. <span data-ttu-id="0e11a-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0e11a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-userecho-from-the-gallery"></a><span data-ttu-id="0e11a-123">Adding UserEcho from the gallery</span><span class="sxs-lookup"><span data-stu-id="0e11a-123">Adding UserEcho from the gallery</span></span>
<span data-ttu-id="0e11a-124">To configure the integration of UserEcho into Azure AD, you need to add UserEcho from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="0e11a-124">To configure the integration of UserEcho into Azure AD, you need to add UserEcho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0e11a-125">**To add UserEcho from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0e11a-125">**To add UserEcho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0e11a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0e11a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="0e11a-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0e11a-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="0e11a-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="0e11a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="0e11a-133">In the search box, type **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-133">In the search box, type **UserEcho**.</span></span>

    ![Creating an Azure AD test user](./media/userecho-tutorial/tutorial_userecho_search.png)

1. <span data-ttu-id="0e11a-135">In the results panel, select **UserEcho**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="0e11a-135">In the results panel, select **UserEcho**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/userecho-tutorial/tutorial_userecho_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0e11a-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0e11a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0e11a-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="0e11a-138">In this section, you configure and test Azure AD single sign-on with UserEcho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0e11a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UserEcho is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e11a-139">For single sign-on to work, Azure AD needs to know what the counterpart user in UserEcho is to a user in Azure AD.</span></span> <span data-ttu-id="0e11a-140">In other words, a link relationship between an Azure AD user and the related user in UserEcho needs to be established.</span><span class="sxs-lookup"><span data-stu-id="0e11a-140">In other words, a link relationship between an Azure AD user and the related user in UserEcho needs to be established.</span></span>

<span data-ttu-id="0e11a-141">In UserEcho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="0e11a-141">In UserEcho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0e11a-142">To configure and test Azure AD single sign-on with UserEcho, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0e11a-142">To configure and test Azure AD single sign-on with UserEcho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0e11a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="0e11a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="0e11a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e11a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="0e11a-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - to have a counterpart of Britta Simon in UserEcho that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="0e11a-145">**[Creating a UserEcho test user](#creating-a-userecho-test-user)** - to have a counterpart of Britta Simon in UserEcho that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="0e11a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0e11a-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="0e11a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="0e11a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0e11a-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0e11a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0e11a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserEcho application.</span><span class="sxs-lookup"><span data-stu-id="0e11a-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your UserEcho application.</span></span>

<span data-ttu-id="0e11a-150">**To configure Azure AD single sign-on with UserEcho, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0e11a-150">**To configure Azure AD single sign-on with UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="0e11a-151">In the Azure portal, on the **UserEcho** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-151">In the Azure portal, on the **UserEcho** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="0e11a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0e11a-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_samlbase.png)

1. <span data-ttu-id="0e11a-155">On the **UserEcho Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0e11a-155">On the **UserEcho Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_url.png)

    <span data-ttu-id="0e11a-157">a.</span><span class="sxs-lookup"><span data-stu-id="0e11a-157">a.</span></span> <span data-ttu-id="0e11a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/`</span><span class="sxs-lookup"><span data-stu-id="0e11a-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/`</span></span>

    <span data-ttu-id="0e11a-159">b.</span><span class="sxs-lookup"><span data-stu-id="0e11a-159">b.</span></span> <span data-ttu-id="0e11a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="0e11a-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.userecho.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0e11a-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="0e11a-161">These values are not real.</span></span> <span data-ttu-id="0e11a-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="0e11a-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="0e11a-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="0e11a-163">Contact [UserEcho Client support team](https://feedback.userecho.com/) to get these values.</span></span> 

1. <span data-ttu-id="0e11a-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="0e11a-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_certificate.png) 

1. <span data-ttu-id="0e11a-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="0e11a-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="0e11a-168">On the **UserEcho Configuration** section, click **Configure UserEcho** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="0e11a-168">On the **UserEcho Configuration** section, click **Configure UserEcho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0e11a-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="0e11a-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_configure.png) 

1. <span data-ttu-id="0e11a-171">In another browser window, sign on to your UserEcho company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0e11a-171">In another browser window, sign on to your UserEcho company site as an administrator.</span></span>

1. <span data-ttu-id="0e11a-172">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-172">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_06.png) 

1. <span data-ttu-id="0e11a-174">Click **Integrations**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-174">Click **Integrations**.</span></span>
   
    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_07.png) 

1. <span data-ttu-id="0e11a-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-176">Click **Website**, and then click **Single sign-on (SAML2)**.</span></span>
   
    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_08.png) 

1. <span data-ttu-id="0e11a-178">On the **Single sign-on (SAML)** page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0e11a-178">On the **Single sign-on (SAML)** page, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_09.png)
    
    <span data-ttu-id="0e11a-180">a.</span><span class="sxs-lookup"><span data-stu-id="0e11a-180">a.</span></span> <span data-ttu-id="0e11a-181">As **SAML-enabled**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-181">As **SAML-enabled**, select **Yes**.</span></span>
    
    <span data-ttu-id="0e11a-182">b.</span><span class="sxs-lookup"><span data-stu-id="0e11a-182">b.</span></span> <span data-ttu-id="0e11a-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SAML SSO URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="0e11a-183">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal into the **SAML SSO URL** textbox.</span></span>
    
    <span data-ttu-id="0e11a-184">c.</span><span class="sxs-lookup"><span data-stu-id="0e11a-184">c.</span></span> <span data-ttu-id="0e11a-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Remote logoout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="0e11a-185">Paste **Sign-Out URL**, which you have copied from the Azure portal into the **Remote logoout URL** textbox.</span></span>
    
    <span data-ttu-id="0e11a-186">d.</span><span class="sxs-lookup"><span data-stu-id="0e11a-186">d.</span></span> <span data-ttu-id="0e11a-187">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **X.509 Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="0e11a-187">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
    
    <span data-ttu-id="0e11a-188">e.</span><span class="sxs-lookup"><span data-stu-id="0e11a-188">e.</span></span> <span data-ttu-id="0e11a-189">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-189">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0e11a-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="0e11a-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0e11a-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="0e11a-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0e11a-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0e11a-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0e11a-193">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0e11a-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="0e11a-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e11a-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="0e11a-196">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0e11a-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0e11a-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0e11a-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/userecho-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="0e11a-199">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/userecho-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="0e11a-201">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="0e11a-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/userecho-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="0e11a-203">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0e11a-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/userecho-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0e11a-205">a.</span><span class="sxs-lookup"><span data-stu-id="0e11a-205">a.</span></span> <span data-ttu-id="0e11a-206">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0e11a-207">b.</span><span class="sxs-lookup"><span data-stu-id="0e11a-207">b.</span></span> <span data-ttu-id="0e11a-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0e11a-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0e11a-209">c.</span><span class="sxs-lookup"><span data-stu-id="0e11a-209">c.</span></span> <span data-ttu-id="0e11a-210">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0e11a-211">d.</span><span class="sxs-lookup"><span data-stu-id="0e11a-211">d.</span></span> <span data-ttu-id="0e11a-212">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-212">Click **Create**.</span></span>
 
### <a name="creating-a-userecho-test-user"></a><span data-ttu-id="0e11a-213">Creating a UserEcho test user</span><span class="sxs-lookup"><span data-stu-id="0e11a-213">Creating a UserEcho test user</span></span>

<span data-ttu-id="0e11a-214">The objective of this section is to create a user called Britta Simon in UserEcho.</span><span class="sxs-lookup"><span data-stu-id="0e11a-214">The objective of this section is to create a user called Britta Simon in UserEcho.</span></span>

<span data-ttu-id="0e11a-215">**To create a user called Britta Simon in UserEcho, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0e11a-215">**To create a user called Britta Simon in UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="0e11a-216">Sign-on to your UserEcho company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0e11a-216">Sign-on to your UserEcho company site as an administrator.</span></span>

1. <span data-ttu-id="0e11a-217">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-217">In the toolbar on the top, click your user name to expand the menu, and then click **Setup**.</span></span>
   
    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_06.png)

1. <span data-ttu-id="0e11a-219">Click **Users**, to expand the **Users** section.</span><span class="sxs-lookup"><span data-stu-id="0e11a-219">Click **Users**, to expand the **Users** section.</span></span>
   
    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_10.png)

1. <span data-ttu-id="0e11a-221">Click **Users**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-221">Click **Users**.</span></span>
   
    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_11.png)

1. <span data-ttu-id="0e11a-223">Click **Invite a new user**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-223">Click **Invite a new user**.</span></span>
   
    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_12.png)

1. <span data-ttu-id="0e11a-225">On the **Invite a new user** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0e11a-225">On the **Invite a new user** dialog, perform the following steps:</span></span>
   
    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_13.png)

    <span data-ttu-id="0e11a-227">a.</span><span class="sxs-lookup"><span data-stu-id="0e11a-227">a.</span></span> <span data-ttu-id="0e11a-228">In the **Name** textbox, type name of the user like Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0e11a-228">In the **Name** textbox, type name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="0e11a-229">b.</span><span class="sxs-lookup"><span data-stu-id="0e11a-229">b.</span></span>  <span data-ttu-id="0e11a-230">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="0e11a-230">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="0e11a-231">c.</span><span class="sxs-lookup"><span data-stu-id="0e11a-231">c.</span></span> <span data-ttu-id="0e11a-232">Click **Invite**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-232">Click **Invite**.</span></span>

<span data-ttu-id="0e11a-233">An invitation is sent to Britta, which enables her to start using UserEcho.</span><span class="sxs-lookup"><span data-stu-id="0e11a-233">An invitation is sent to Britta, which enables her to start using UserEcho.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0e11a-234">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0e11a-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0e11a-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserEcho.</span><span class="sxs-lookup"><span data-stu-id="0e11a-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to UserEcho.</span></span>

![Assign User][200] 

<span data-ttu-id="0e11a-237">**To assign Britta Simon to UserEcho, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0e11a-237">**To assign Britta Simon to UserEcho, perform the following steps:**</span></span>

1. <span data-ttu-id="0e11a-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="0e11a-240">In the applications list, select **UserEcho**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-240">In the applications list, select **UserEcho**.</span></span>

    ![Configure Single Sign-On](./media/userecho-tutorial/tutorial_userecho_app.png) 

1. <span data-ttu-id="0e11a-242">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0e11a-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="0e11a-244">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0e11a-244">Click **Add** button.</span></span> <span data-ttu-id="0e11a-245">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0e11a-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="0e11a-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="0e11a-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="0e11a-248">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="0e11a-248">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="0e11a-249">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0e11a-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0e11a-250">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="0e11a-250">Testing single sign-on</span></span>

<span data-ttu-id="0e11a-251">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0e11a-251">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="0e11a-252">When you click the UserEcho tile in the Access Panel, you should get automatically signed-on to your UserEcho application.</span><span class="sxs-lookup"><span data-stu-id="0e11a-252">When you click the UserEcho tile in the Access Panel, you should get automatically signed-on to your UserEcho application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0e11a-253">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0e11a-253">Additional resources</span></span>

* [<span data-ttu-id="0e11a-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0e11a-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="0e11a-255">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0e11a-255">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/userecho-tutorial/tutorial_general_01.png
[2]: ./media/userecho-tutorial/tutorial_general_02.png
[3]: ./media/userecho-tutorial/tutorial_general_03.png
[4]: ./media/userecho-tutorial/tutorial_general_04.png

[100]: ./media/userecho-tutorial/tutorial_general_100.png

[200]: ./media/userecho-tutorial/tutorial_general_200.png
[201]: ./media/userecho-tutorial/tutorial_general_201.png
[202]: ./media/userecho-tutorial/tutorial_general_202.png
[203]: ./media/userecho-tutorial/tutorial_general_203.png

