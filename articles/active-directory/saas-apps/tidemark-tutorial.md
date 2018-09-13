---
title: 'Tutorial: Azure Active Directory integration with Tidemark | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Tidemark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 5cf80d4e-6e8b-48ec-81c8-27872af5e5d5
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: d99dc053849ef4e42db8486613c699de57a5c7c6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858134"
---
# <a name="tutorial-azure-active-directory-integration-with-tidemark"></a><span data-ttu-id="f3d6c-103">Tutorial: Azure Active Directory integration with Tidemark</span><span class="sxs-lookup"><span data-stu-id="f3d6c-103">Tutorial: Azure Active Directory integration with Tidemark</span></span>

<span data-ttu-id="f3d6c-104">In this tutorial, you learn how to integrate Tidemark with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f3d6c-104">In this tutorial, you learn how to integrate Tidemark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f3d6c-105">Integrating Tidemark with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f3d6c-105">Integrating Tidemark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f3d6c-106">You can control in Azure AD who has access to Tidemark</span><span class="sxs-lookup"><span data-stu-id="f3d6c-106">You can control in Azure AD who has access to Tidemark</span></span>
- <span data-ttu-id="f3d6c-107">You can enable your users to automatically get signed-on to Tidemark (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="f3d6c-107">You can enable your users to automatically get signed-on to Tidemark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f3d6c-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f3d6c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f3d6c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="f3d6c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f3d6c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f3d6c-110">Prerequisites</span></span>

<span data-ttu-id="f3d6c-111">To configure Azure AD integration with Tidemark, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="f3d6c-111">To configure Azure AD integration with Tidemark, you need the following items:</span></span>

- <span data-ttu-id="f3d6c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="f3d6c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f3d6c-113">A Tidemark single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="f3d6c-113">A Tidemark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f3d6c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f3d6c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="f3d6c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f3d6c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f3d6c-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f3d6c-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f3d6c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="f3d6c-118">Scenario description</span></span>
<span data-ttu-id="f3d6c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f3d6c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="f3d6c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f3d6c-121">Adding Tidemark from the gallery</span><span class="sxs-lookup"><span data-stu-id="f3d6c-121">Adding Tidemark from the gallery</span></span>
1. <span data-ttu-id="f3d6c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f3d6c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tidemark-from-the-gallery"></a><span data-ttu-id="f3d6c-123">Adding Tidemark from the gallery</span><span class="sxs-lookup"><span data-stu-id="f3d6c-123">Adding Tidemark from the gallery</span></span>
<span data-ttu-id="f3d6c-124">To configure the integration of Tidemark into Azure AD, you need to add Tidemark from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-124">To configure the integration of Tidemark into Azure AD, you need to add Tidemark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f3d6c-125">**To add Tidemark from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f3d6c-125">**To add Tidemark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f3d6c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="f3d6c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f3d6c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="f3d6c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="f3d6c-133">In the search box, type **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-133">In the search box, type **Tidemark**.</span></span>

    ![Creating an Azure AD test user](./media/tidemark-tutorial/tutorial_tidemark_search.png)

1. <span data-ttu-id="f3d6c-135">In the results panel, select **Tidemark**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-135">In the results panel, select **Tidemark**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/tidemark-tutorial/tutorial_tidemark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f3d6c-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f3d6c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f3d6c-138">In this section, you configure and test Azure AD single sign-on with Tidemark based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="f3d6c-138">In this section, you configure and test Azure AD single sign-on with Tidemark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f3d6c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tidemark is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Tidemark is to a user in Azure AD.</span></span> <span data-ttu-id="f3d6c-140">In other words, a link relationship between an Azure AD user and the related user in Tidemark needs to be established.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-140">In other words, a link relationship between an Azure AD user and the related user in Tidemark needs to be established.</span></span>

<span data-ttu-id="f3d6c-141">In Tidemark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-141">In Tidemark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f3d6c-142">To configure and test Azure AD single sign-on with Tidemark, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="f3d6c-142">To configure and test Azure AD single sign-on with Tidemark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f3d6c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="f3d6c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="f3d6c-145">**[Creating a Tidemark test user](#creating-a-tidemark-test-user)** - to have a counterpart of Britta Simon in Tidemark that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-145">**[Creating a Tidemark test user](#creating-a-tidemark-test-user)** - to have a counterpart of Britta Simon in Tidemark that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="f3d6c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="f3d6c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f3d6c-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="f3d6c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f3d6c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tidemark application.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Tidemark application.</span></span>

<span data-ttu-id="f3d6c-150">**To configure Azure AD single sign-on with Tidemark, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f3d6c-150">**To configure Azure AD single sign-on with Tidemark, perform the following steps:**</span></span>

1. <span data-ttu-id="f3d6c-151">In the Azure portal, on the **Tidemark** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-151">In the Azure portal, on the **Tidemark** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="f3d6c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/tidemark-tutorial/tutorial_tidemark_samlbase.png)

1. <span data-ttu-id="f3d6c-155">On the **Tidemark Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f3d6c-155">On the **Tidemark Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/tidemark-tutorial/tutorial_tidemark_url.png)

    <span data-ttu-id="f3d6c-157">a.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-157">a.</span></span> <span data-ttu-id="f3d6c-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="f3d6c-158">In the **Sign-on URL** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/login` |
    | `https://<subdomain>.tidemark.net/login` |

    <span data-ttu-id="f3d6c-159">b.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-159">b.</span></span> <span data-ttu-id="f3d6c-160">In the **Identifier** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="f3d6c-160">In the **Identifier** textbox, type a URL using the following patterns:</span></span> 
    | |
    |--|
    | `https://<subdomain>.tidemark.com/saml` |
    | `https://<subdomain>.tidemark.net/saml` |

    > [!NOTE] 
    > <span data-ttu-id="f3d6c-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-161">These values are not real.</span></span> <span data-ttu-id="f3d6c-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f3d6c-163">Contact [Tidemark Client support team](http://www.tidemark.com/contact-us) to get these values.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-163">Contact [Tidemark Client support team](http://www.tidemark.com/contact-us) to get these values.</span></span> 
 
1. <span data-ttu-id="f3d6c-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/tidemark-tutorial/tutorial_tidemark_certificate.png) 

1. <span data-ttu-id="f3d6c-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/tidemark-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="f3d6c-168">On the **Tidemark Configuration** section, click **Configure Tidemark** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-168">On the **Tidemark Configuration** section, click **Configure Tidemark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f3d6c-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="f3d6c-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/tidemark-tutorial/tutorial_tidemark_configure.png) 

1. <span data-ttu-id="f3d6c-171">To configure single sign-on on **Tidemark** side, you need to send the downloaded **Certificate(Base64), SAML Entity ID, Sign-Out URL and SAML Single Sign-On Service URL** to [Tidemark support team](http://www.tidemark.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="f3d6c-171">To configure single sign-on on **Tidemark** side, you need to send the downloaded **Certificate(Base64), SAML Entity ID, Sign-Out URL and SAML Single Sign-On Service URL** to [Tidemark support team](http://www.tidemark.com/contact-us).</span></span> <span data-ttu-id="f3d6c-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="f3d6c-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="f3d6c-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f3d6c-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f3d6c-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f3d6c-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f3d6c-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f3d6c-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="f3d6c-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="f3d6c-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f3d6c-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f3d6c-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/tidemark-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="f3d6c-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/tidemark-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="f3d6c-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/tidemark-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="f3d6c-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="f3d6c-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/tidemark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f3d6c-188">a.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-188">a.</span></span> <span data-ttu-id="f3d6c-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f3d6c-190">b.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-190">b.</span></span> <span data-ttu-id="f3d6c-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f3d6c-192">c.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-192">c.</span></span> <span data-ttu-id="f3d6c-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f3d6c-194">d.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-194">d.</span></span> <span data-ttu-id="f3d6c-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-195">Click **Create**.</span></span>
 
### <a name="creating-a-tidemark-test-user"></a><span data-ttu-id="f3d6c-196">Creating a Tidemark test user</span><span class="sxs-lookup"><span data-stu-id="f3d6c-196">Creating a Tidemark test user</span></span>

<span data-ttu-id="f3d6c-197">The objective of this section is to create a user called Britta Simon in Tidemark.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-197">The objective of this section is to create a user called Britta Simon in Tidemark.</span></span> <span data-ttu-id="f3d6c-198">Please work with [Tidemark support team](http://www.tidemark.com/contact-us) to add the users in the Tidemark account.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-198">Please work with [Tidemark support team](http://www.tidemark.com/contact-us) to add the users in the Tidemark account.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f3d6c-199">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="f3d6c-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f3d6c-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tidemark.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Tidemark.</span></span>

![Assign User][200] 

<span data-ttu-id="f3d6c-202">**To assign Britta Simon to Tidemark, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="f3d6c-202">**To assign Britta Simon to Tidemark, perform the following steps:**</span></span>

1. <span data-ttu-id="f3d6c-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="f3d6c-205">In the applications list, select **Tidemark**.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-205">In the applications list, select **Tidemark**.</span></span>

    ![Configure Single Sign-On](./media/tidemark-tutorial/tutorial_tidemark_app.png) 

1. <span data-ttu-id="f3d6c-207">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="f3d6c-209">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-209">Click **Add** button.</span></span> <span data-ttu-id="f3d6c-210">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="f3d6c-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="f3d6c-213">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-213">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="f3d6c-214">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f3d6c-215">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="f3d6c-215">Testing single sign-on</span></span>

<span data-ttu-id="f3d6c-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f3d6c-217">When you click the Tidemark tile in the Access Panel, you should get automatically signed-on to your Tidemark application.</span><span class="sxs-lookup"><span data-stu-id="f3d6c-217">When you click the Tidemark tile in the Access Panel, you should get automatically signed-on to your Tidemark application.</span></span>
<span data-ttu-id="f3d6c-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f3d6c-218">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f3d6c-219">Additional resources</span><span class="sxs-lookup"><span data-stu-id="f3d6c-219">Additional resources</span></span>

* [<span data-ttu-id="f3d6c-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3d6c-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="f3d6c-221">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f3d6c-221">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/tidemark-tutorial/tutorial_general_01.png
[2]: ./media/tidemark-tutorial/tutorial_general_02.png
[3]: ./media/tidemark-tutorial/tutorial_general_03.png
[4]: ./media/tidemark-tutorial/tutorial_general_04.png

[100]: ./media/tidemark-tutorial/tutorial_general_100.png

[200]: ./media/tidemark-tutorial/tutorial_general_200.png
[201]: ./media/tidemark-tutorial/tutorial_general_201.png
[202]: ./media/tidemark-tutorial/tutorial_general_202.png
[203]: ./media/tidemark-tutorial/tutorial_general_203.png

