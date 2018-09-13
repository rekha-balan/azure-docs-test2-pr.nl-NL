---
title: 'Tutorial: Azure Active Directory integration with Picturepark | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Picturepark.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 2414240d3ab4b5cedce734579f0d39a3df59c3cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857054"
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="cc73b-103">Tutorial: Azure Active Directory integration with Picturepark</span><span class="sxs-lookup"><span data-stu-id="cc73b-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="cc73b-104">In this tutorial, you learn how to integrate Picturepark with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cc73b-104">In this tutorial, you learn how to integrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cc73b-105">Integrating Picturepark with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="cc73b-105">Integrating Picturepark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cc73b-106">You can control in Azure AD who has access to Picturepark</span><span class="sxs-lookup"><span data-stu-id="cc73b-106">You can control in Azure AD who has access to Picturepark</span></span>
- <span data-ttu-id="cc73b-107">You can enable your users to automatically get signed-on to Picturepark (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="cc73b-107">You can enable your users to automatically get signed-on to Picturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cc73b-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cc73b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cc73b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="cc73b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc73b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cc73b-110">Prerequisites</span></span>

<span data-ttu-id="cc73b-111">To configure Azure AD integration with Picturepark, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="cc73b-111">To configure Azure AD integration with Picturepark, you need the following items:</span></span>

- <span data-ttu-id="cc73b-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="cc73b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cc73b-113">A Picturepark single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="cc73b-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cc73b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="cc73b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cc73b-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="cc73b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cc73b-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="cc73b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cc73b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc73b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cc73b-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="cc73b-118">Scenario description</span></span>
<span data-ttu-id="cc73b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="cc73b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cc73b-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="cc73b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cc73b-121">Adding Picturepark from the gallery</span><span class="sxs-lookup"><span data-stu-id="cc73b-121">Adding Picturepark from the gallery</span></span>
1. <span data-ttu-id="cc73b-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc73b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-the-gallery"></a><span data-ttu-id="cc73b-123">Adding Picturepark from the gallery</span><span class="sxs-lookup"><span data-stu-id="cc73b-123">Adding Picturepark from the gallery</span></span>
<span data-ttu-id="cc73b-124">To configure the integration of Picturepark into Azure AD, you need to add Picturepark from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="cc73b-124">To configure the integration of Picturepark into Azure AD, you need to add Picturepark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cc73b-125">**To add Picturepark from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc73b-125">**To add Picturepark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cc73b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cc73b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="cc73b-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cc73b-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="cc73b-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="cc73b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="cc73b-133">In the search box, type **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-133">In the search box, type **Picturepark**.</span></span>

    ![Creating an Azure AD test user](./media/picturepark-tutorial/tutorial_picturepark_search.png)

1. <span data-ttu-id="cc73b-135">In the results panel, select **Picturepark**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="cc73b-135">In the results panel, select **Picturepark**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cc73b-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc73b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cc73b-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="cc73b-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cc73b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Picturepark is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cc73b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Picturepark is to a user in Azure AD.</span></span> <span data-ttu-id="cc73b-140">In other words, a link relationship between an Azure AD user and the related user in Picturepark needs to be established.</span><span class="sxs-lookup"><span data-stu-id="cc73b-140">In other words, a link relationship between an Azure AD user and the related user in Picturepark needs to be established.</span></span>

<span data-ttu-id="cc73b-141">In Picturepark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="cc73b-141">In Picturepark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cc73b-142">To configure and test Azure AD single sign-on with Picturepark, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="cc73b-142">To configure and test Azure AD single sign-on with Picturepark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cc73b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="cc73b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="cc73b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc73b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="cc73b-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - to have a counterpart of Britta Simon in Picturepark that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="cc73b-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - to have a counterpart of Britta Simon in Picturepark that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="cc73b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc73b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="cc73b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="cc73b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cc73b-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc73b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cc73b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Picturepark application.</span><span class="sxs-lookup"><span data-stu-id="cc73b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="cc73b-150">**To configure Azure AD single sign-on with Picturepark, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc73b-150">**To configure Azure AD single sign-on with Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="cc73b-151">In the Azure portal, on the **Picturepark** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-151">In the Azure portal, on the **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="cc73b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="cc73b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/picturepark-tutorial/tutorial_picturepark_samlbase.png)

1. <span data-ttu-id="cc73b-155">On the **Picturepark Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cc73b-155">On the **Picturepark Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="cc73b-157">a.</span><span class="sxs-lookup"><span data-stu-id="cc73b-157">a.</span></span> <span data-ttu-id="cc73b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="cc73b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="cc73b-159">b.</span><span class="sxs-lookup"><span data-stu-id="cc73b-159">b.</span></span> <span data-ttu-id="cc73b-160">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="cc73b-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="cc73b-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="cc73b-161">These values are not real.</span></span> <span data-ttu-id="cc73b-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="cc73b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="cc73b-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="cc73b-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) to get these values.</span></span> 
 
1. <span data-ttu-id="cc73b-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span><span class="sxs-lookup"><span data-stu-id="cc73b-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Configure Single Sign-On](./media/picturepark-tutorial/tutorial_picturepark_certificate.png) 

1. <span data-ttu-id="cc73b-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="cc73b-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/picturepark-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="cc73b-168">On the **Picturepark Configuration** section, click **Configure Picturepark** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="cc73b-168">On the **Picturepark Configuration** section, click **Configure Picturepark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="cc73b-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="cc73b-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/picturepark-tutorial/tutorial_picturepark_configure.png) 

1. <span data-ttu-id="cc73b-171">In a different web browser window, log into your Picturepark company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="cc73b-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

1. <span data-ttu-id="cc73b-172">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-172">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="cc73b-173">![Management Console](./media/picturepark-tutorial/ic795062.png "Management Console")</span><span class="sxs-lookup"><span data-stu-id="cc73b-173">![Management Console](./media/picturepark-tutorial/ic795062.png "Management Console")</span></span>

1. <span data-ttu-id="cc73b-174">Click **Authentication**, and then click **Identity providers**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="cc73b-175">![Authentication](./media/picturepark-tutorial/ic795063.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="cc73b-175">![Authentication](./media/picturepark-tutorial/ic795063.png "Authentication")</span></span>

1. <span data-ttu-id="cc73b-176">In the **Identity provider configuration** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cc73b-176">In the **Identity provider configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="cc73b-177">![Identity provider configuration](./media/picturepark-tutorial/ic795064.png "Identity provider configuration")</span><span class="sxs-lookup"><span data-stu-id="cc73b-177">![Identity provider configuration](./media/picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="cc73b-178">a.</span><span class="sxs-lookup"><span data-stu-id="cc73b-178">a.</span></span> <span data-ttu-id="cc73b-179">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-179">Click **Add**.</span></span>
  
    <span data-ttu-id="cc73b-180">b.</span><span class="sxs-lookup"><span data-stu-id="cc73b-180">b.</span></span> <span data-ttu-id="cc73b-181">Type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="cc73b-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="cc73b-182">c.</span><span class="sxs-lookup"><span data-stu-id="cc73b-182">c.</span></span> <span data-ttu-id="cc73b-183">Select **Set as default**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="cc73b-184">d.</span><span class="sxs-lookup"><span data-stu-id="cc73b-184">d.</span></span> <span data-ttu-id="cc73b-185">In **Issuer URI** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cc73b-185">In **Issuer URI** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="cc73b-186">e.</span><span class="sxs-lookup"><span data-stu-id="cc73b-186">e.</span></span> <span data-ttu-id="cc73b-187">In **Trusted Issuer Thumb Print** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span><span class="sxs-lookup"><span data-stu-id="cc73b-187">In **Trusted Issuer Thumb Print** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

1. <span data-ttu-id="cc73b-188">Click **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-188">Click **JoinDefaultUsersGroup**.</span></span>

1. <span data-ttu-id="cc73b-189">To set the **Emailaddress** attribute in the **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-189">To set the **Emailaddress** attribute in the **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="cc73b-190">![Configuration](./media/picturepark-tutorial/ic795065.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="cc73b-190">![Configuration](./media/picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="cc73b-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="cc73b-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cc73b-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="cc73b-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cc73b-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="cc73b-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cc73b-194">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cc73b-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="cc73b-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cc73b-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="cc73b-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc73b-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cc73b-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="cc73b-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/picturepark-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="cc73b-200">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/picturepark-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="cc73b-202">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="cc73b-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/picturepark-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="cc73b-204">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="cc73b-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cc73b-206">a.</span><span class="sxs-lookup"><span data-stu-id="cc73b-206">a.</span></span> <span data-ttu-id="cc73b-207">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cc73b-208">b.</span><span class="sxs-lookup"><span data-stu-id="cc73b-208">b.</span></span> <span data-ttu-id="cc73b-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc73b-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cc73b-210">c.</span><span class="sxs-lookup"><span data-stu-id="cc73b-210">c.</span></span> <span data-ttu-id="cc73b-211">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cc73b-212">d.</span><span class="sxs-lookup"><span data-stu-id="cc73b-212">d.</span></span> <span data-ttu-id="cc73b-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="cc73b-214">Creating a Picturepark test user</span><span class="sxs-lookup"><span data-stu-id="cc73b-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="cc73b-215">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span><span class="sxs-lookup"><span data-stu-id="cc73b-215">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="cc73b-216">In the case of Picturepark, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="cc73b-216">In the case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="cc73b-217">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc73b-217">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="cc73b-218">Log in to your **Picturepark** tenant.</span><span class="sxs-lookup"><span data-stu-id="cc73b-218">Log in to your **Picturepark** tenant.</span></span>

1. <span data-ttu-id="cc73b-219">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-219">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="cc73b-220">![Users](./media/picturepark-tutorial/ic795067.png "Users")</span><span class="sxs-lookup"><span data-stu-id="cc73b-220">![Users](./media/picturepark-tutorial/ic795067.png "Users")</span></span>

1. <span data-ttu-id="cc73b-221">In the **Users overview** tab, click **New**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-221">In the **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="cc73b-222">![User management](./media/picturepark-tutorial/ic795068.png "User management")</span><span class="sxs-lookup"><span data-stu-id="cc73b-222">![User management](./media/picturepark-tutorial/ic795068.png "User management")</span></span>

1. <span data-ttu-id="cc73b-223">On the **Create User** dialog, perform the following steps of a valid Azure Active Directory User you want to provision:</span><span class="sxs-lookup"><span data-stu-id="cc73b-223">On the **Create User** dialog, perform the following steps of a valid Azure Active Directory User you want to provision:</span></span>
   
    <span data-ttu-id="cc73b-224">![Create User](./media/picturepark-tutorial/ic795069.png "Create User")</span><span class="sxs-lookup"><span data-stu-id="cc73b-224">![Create User](./media/picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="cc73b-225">a.</span><span class="sxs-lookup"><span data-stu-id="cc73b-225">a.</span></span> <span data-ttu-id="cc73b-226">In the **Email Address** textbox, type the **email address** of the user **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-226">In the **Email Address** textbox, type the **email address** of the user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="cc73b-227">b.</span><span class="sxs-lookup"><span data-stu-id="cc73b-227">b.</span></span> <span data-ttu-id="cc73b-228">In the **Password** and **Confirm Password** textboxes, type the **password** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cc73b-228">In the **Password** and **Confirm Password** textboxes, type the **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="cc73b-229">c.</span><span class="sxs-lookup"><span data-stu-id="cc73b-229">c.</span></span> <span data-ttu-id="cc73b-230">In the **First Name** textbox, type the **First Name** of the user **Britta**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-230">In the **First Name** textbox, type the **First Name** of the user **Britta**.</span></span> 
   
    <span data-ttu-id="cc73b-231">d.</span><span class="sxs-lookup"><span data-stu-id="cc73b-231">d.</span></span> <span data-ttu-id="cc73b-232">In the **Last Name** textbox, type the **Last Name** of the user **Simon**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-232">In the **Last Name** textbox, type the **Last Name** of the user **Simon**.</span></span>
   
    <span data-ttu-id="cc73b-233">e.</span><span class="sxs-lookup"><span data-stu-id="cc73b-233">e.</span></span> <span data-ttu-id="cc73b-234">In the **Company** textbox, type the **Company name** of the user.</span><span class="sxs-lookup"><span data-stu-id="cc73b-234">In the **Company** textbox, type the **Company name** of the user.</span></span> 
   
    <span data-ttu-id="cc73b-235">f.</span><span class="sxs-lookup"><span data-stu-id="cc73b-235">f.</span></span> <span data-ttu-id="cc73b-236">In the **Country** textbox, select the **Country** of the user.</span><span class="sxs-lookup"><span data-stu-id="cc73b-236">In the **Country** textbox, select the **Country** of the user.</span></span>
  
    <span data-ttu-id="cc73b-237">g.</span><span class="sxs-lookup"><span data-stu-id="cc73b-237">g.</span></span> <span data-ttu-id="cc73b-238">In the **ZIP** textbox, type the **ZIP code** of the city.</span><span class="sxs-lookup"><span data-stu-id="cc73b-238">In the **ZIP** textbox, type the **ZIP code** of the city.</span></span>
   
    <span data-ttu-id="cc73b-239">h.</span><span class="sxs-lookup"><span data-stu-id="cc73b-239">h.</span></span> <span data-ttu-id="cc73b-240">In the **City** textbox, type the **City name** of the user.</span><span class="sxs-lookup"><span data-stu-id="cc73b-240">In the **City** textbox, type the **City name** of the user.</span></span>

    <span data-ttu-id="cc73b-241">i.</span><span class="sxs-lookup"><span data-stu-id="cc73b-241">i.</span></span> <span data-ttu-id="cc73b-242">Select a **Language**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="cc73b-243">j.</span><span class="sxs-lookup"><span data-stu-id="cc73b-243">j.</span></span> <span data-ttu-id="cc73b-244">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="cc73b-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="cc73b-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cc73b-246">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="cc73b-246">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cc73b-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Picturepark.</span><span class="sxs-lookup"><span data-stu-id="cc73b-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Picturepark.</span></span>

![Assign User][200] 

<span data-ttu-id="cc73b-249">**To assign Britta Simon to Picturepark, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="cc73b-249">**To assign Britta Simon to Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="cc73b-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="cc73b-252">In the applications list, select **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-252">In the applications list, select **Picturepark**.</span></span>

    ![Configure Single Sign-On](./media/picturepark-tutorial/tutorial_picturepark_app.png) 

1. <span data-ttu-id="cc73b-254">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="cc73b-254">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="cc73b-256">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="cc73b-256">Click **Add** button.</span></span> <span data-ttu-id="cc73b-257">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cc73b-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="cc73b-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="cc73b-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="cc73b-260">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="cc73b-260">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="cc73b-261">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="cc73b-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cc73b-262">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="cc73b-262">Testing single sign-on</span></span>

<span data-ttu-id="cc73b-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="cc73b-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="cc73b-264">When you click the Picturepark tile in the Access Panel, you should get automatically signed-on to your Picturepark application.</span><span class="sxs-lookup"><span data-stu-id="cc73b-264">When you click the Picturepark tile in the Access Panel, you should get automatically signed-on to your Picturepark application.</span></span> <span data-ttu-id="cc73b-265">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc73b-265">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cc73b-266">Additional resources</span><span class="sxs-lookup"><span data-stu-id="cc73b-266">Additional resources</span></span>

* [<span data-ttu-id="cc73b-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cc73b-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="cc73b-268">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cc73b-268">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/picturepark-tutorial/tutorial_general_01.png
[2]: ./media/picturepark-tutorial/tutorial_general_02.png
[3]: ./media/picturepark-tutorial/tutorial_general_03.png
[4]: ./media/picturepark-tutorial/tutorial_general_04.png

[100]: ./media/picturepark-tutorial/tutorial_general_100.png

[200]: ./media/picturepark-tutorial/tutorial_general_200.png
[201]: ./media/picturepark-tutorial/tutorial_general_201.png
[202]: ./media/picturepark-tutorial/tutorial_general_202.png
[203]: ./media/picturepark-tutorial/tutorial_general_203.png

