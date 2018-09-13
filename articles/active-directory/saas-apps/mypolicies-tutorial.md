---
title: 'Tutorial: Azure Active Directory integration with myPolicies | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and myPolicies.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: bf79e858-1dfb-4ab3-a6df-74b2d5a878d2
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/04/2017
ms.author: jeedes
ms.openlocfilehash: f4c34d224c65a6e339f12def01079a87247d2d60
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864775"
---
# <a name="tutorial-azure-active-directory-integration-with-mypolicies"></a><span data-ttu-id="91c33-103">Tutorial: Azure Active Directory integration with myPolicies</span><span class="sxs-lookup"><span data-stu-id="91c33-103">Tutorial: Azure Active Directory integration with myPolicies</span></span>

<span data-ttu-id="91c33-104">In this tutorial, you learn how to integrate myPolicies with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="91c33-104">In this tutorial, you learn how to integrate myPolicies with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="91c33-105">Integrating myPolicies with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="91c33-105">Integrating myPolicies with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="91c33-106">You can control in Azure AD who has access to myPolicies</span><span class="sxs-lookup"><span data-stu-id="91c33-106">You can control in Azure AD who has access to myPolicies</span></span>
- <span data-ttu-id="91c33-107">You can enable your users to automatically get signed-on to myPolicies (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="91c33-107">You can enable your users to automatically get signed-on to myPolicies (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="91c33-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="91c33-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="91c33-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="91c33-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91c33-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91c33-110">Prerequisites</span></span>

<span data-ttu-id="91c33-111">To configure Azure AD integration with myPolicies, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="91c33-111">To configure Azure AD integration with myPolicies, you need the following items:</span></span>

- <span data-ttu-id="91c33-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="91c33-112">An Azure AD subscription</span></span>
- <span data-ttu-id="91c33-113">A myPolicies single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="91c33-113">A myPolicies single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="91c33-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="91c33-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="91c33-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="91c33-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="91c33-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="91c33-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="91c33-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="91c33-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="91c33-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="91c33-118">Scenario description</span></span>
<span data-ttu-id="91c33-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="91c33-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="91c33-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="91c33-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="91c33-121">Adding myPolicies from the gallery</span><span class="sxs-lookup"><span data-stu-id="91c33-121">Adding myPolicies from the gallery</span></span>
1. <span data-ttu-id="91c33-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="91c33-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mypolicies-from-the-gallery"></a><span data-ttu-id="91c33-123">Adding myPolicies from the gallery</span><span class="sxs-lookup"><span data-stu-id="91c33-123">Adding myPolicies from the gallery</span></span>
<span data-ttu-id="91c33-124">To configure the integration of myPolicies into Azure AD, you need to add myPolicies from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="91c33-124">To configure the integration of myPolicies into Azure AD, you need to add myPolicies from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="91c33-125">**To add myPolicies from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91c33-125">**To add myPolicies from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="91c33-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="91c33-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="91c33-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="91c33-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="91c33-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="91c33-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="91c33-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="91c33-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="91c33-133">In the search box, type **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="91c33-133">In the search box, type **myPolicies**.</span></span>

    ![Creating an Azure AD test user](./media/mypolicies-tutorial/tutorial_mypolicies_search.png)

1. <span data-ttu-id="91c33-135">In the results panel, select **myPolicies**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="91c33-135">In the results panel, select **myPolicies**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/mypolicies-tutorial/tutorial_mypolicies_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="91c33-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="91c33-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="91c33-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="91c33-138">In this section, you configure and test Azure AD single sign-on with myPolicies based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="91c33-139">For single sign-on to work, Azure AD needs to know what the counterpart user in myPolicies is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="91c33-139">For single sign-on to work, Azure AD needs to know what the counterpart user in myPolicies is to a user in Azure AD.</span></span> <span data-ttu-id="91c33-140">In other words, a link relationship between an Azure AD user and the related user in myPolicies needs to be established.</span><span class="sxs-lookup"><span data-stu-id="91c33-140">In other words, a link relationship between an Azure AD user and the related user in myPolicies needs to be established.</span></span>

<span data-ttu-id="91c33-141">In myPolicies, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="91c33-141">In myPolicies, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="91c33-142">To configure and test Azure AD single sign-on with myPolicies, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="91c33-142">To configure and test Azure AD single sign-on with myPolicies, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="91c33-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="91c33-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="91c33-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91c33-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="91c33-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - to have a counterpart of Britta Simon in myPolicies that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="91c33-145">**[Creating a myPolicies test user](#creating-a-mypolicies-test-user)** - to have a counterpart of Britta Simon in myPolicies that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="91c33-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91c33-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="91c33-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="91c33-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="91c33-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="91c33-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="91c33-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your myPolicies application.</span><span class="sxs-lookup"><span data-stu-id="91c33-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your myPolicies application.</span></span>

<span data-ttu-id="91c33-150">**To configure Azure AD single sign-on with myPolicies, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91c33-150">**To configure Azure AD single sign-on with myPolicies, perform the following steps:**</span></span>

1. <span data-ttu-id="91c33-151">In the Azure portal, on the **myPolicies** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="91c33-151">In the Azure portal, on the **myPolicies** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="91c33-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91c33-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/mypolicies-tutorial/tutorial_mypolicies_samlbase.png)

1. <span data-ttu-id="91c33-155">On the **myPolicies Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91c33-155">On the **myPolicies Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/mypolicies-tutorial/tutorial_mypolicies_url.png)

    <span data-ttu-id="91c33-157">a.</span><span class="sxs-lookup"><span data-stu-id="91c33-157">a.</span></span> <span data-ttu-id="91c33-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/`</span><span class="sxs-lookup"><span data-stu-id="91c33-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/`</span></span>

    <span data-ttu-id="91c33-159">b.</span><span class="sxs-lookup"><span data-stu-id="91c33-159">b.</span></span> <span data-ttu-id="91c33-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="91c33-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<tenantname>.mypolicies.com/users/auth/saml/callback`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="91c33-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="91c33-161">These values are not real.</span></span> <span data-ttu-id="91c33-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="91c33-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="91c33-163">Contact [myPolicies support team](mailto:support@mypolicies.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="91c33-163">Contact [myPolicies support team](mailto:support@mypolicies.com) to get these values.</span></span>

1. <span data-ttu-id="91c33-164">The myPolicies application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span><span class="sxs-lookup"><span data-stu-id="91c33-164">The myPolicies application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="91c33-165">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="91c33-165">Configure the following claims for this application.</span></span> <span data-ttu-id="91c33-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="91c33-166">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="91c33-167">The following screenshot shows an example for this.</span><span class="sxs-lookup"><span data-stu-id="91c33-167">The following screenshot shows an example for this.</span></span> 

    ![Configure Single Sign-On](./media/mypolicies-tutorial/tutorial_mypolicies_attribute.png)

1. <span data-ttu-id="91c33-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span><span class="sxs-lookup"><span data-stu-id="91c33-169">Click **View and edit all other user attributes** checkbox in the **User Attributes** section to expand the attributes.</span></span> <span data-ttu-id="91c33-170">Perform the following steps on each of the displayed attributes-</span><span class="sxs-lookup"><span data-stu-id="91c33-170">Perform the following steps on each of the displayed attributes-</span></span>

    | <span data-ttu-id="91c33-171">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="91c33-171">Attribute Name</span></span> | <span data-ttu-id="91c33-172">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="91c33-172">Attribute Value</span></span> |
    | ------------------- | ---------- |
    | <span data-ttu-id="91c33-173">givenname</span><span class="sxs-lookup"><span data-stu-id="91c33-173">givenname</span></span> | <span data-ttu-id="91c33-174">user.givenname</span><span class="sxs-lookup"><span data-stu-id="91c33-174">user.givenname</span></span> |
    | <span data-ttu-id="91c33-175">surname</span><span class="sxs-lookup"><span data-stu-id="91c33-175">surname</span></span> | <span data-ttu-id="91c33-176">user.surname</span><span class="sxs-lookup"><span data-stu-id="91c33-176">user.surname</span></span> |
    | <span data-ttu-id="91c33-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="91c33-177">emailaddress</span></span> | <span data-ttu-id="91c33-178">user.mail</span><span class="sxs-lookup"><span data-stu-id="91c33-178">user.mail</span></span> |
    | <span data-ttu-id="91c33-179">name</span><span class="sxs-lookup"><span data-stu-id="91c33-179">name</span></span> | <span data-ttu-id="91c33-180">user.userprincipalname</span><span class="sxs-lookup"><span data-stu-id="91c33-180">user.userprincipalname</span></span> |
    
    <span data-ttu-id="91c33-181">a.</span><span class="sxs-lookup"><span data-stu-id="91c33-181">a.</span></span> <span data-ttu-id="91c33-182">Click on the attribute to open the **Edit Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="91c33-182">Click on the attribute to open the **Edit Attribute** dialog.</span></span>
    
    ![Configure Single Sign-On](./media/mypolicies-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="91c33-184">b.</span><span class="sxs-lookup"><span data-stu-id="91c33-184">b.</span></span> <span data-ttu-id="91c33-185">Delete the URL value from the **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="91c33-185">Delete the URL value from the **Namespace**.</span></span>
    
    <span data-ttu-id="91c33-186">c.</span><span class="sxs-lookup"><span data-stu-id="91c33-186">c.</span></span> <span data-ttu-id="91c33-187">Click **Ok** to save the setting.</span><span class="sxs-lookup"><span data-stu-id="91c33-187">Click **Ok** to save the setting.</span></span>
    
1. <span data-ttu-id="91c33-188">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="91c33-188">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/mypolicies-tutorial/tutorial_mypolicies_certificate.png) 

1. <span data-ttu-id="91c33-190">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="91c33-190">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/mypolicies-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="91c33-192">On the **myPolicies Configuration** section, click **Configure myPolicies** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="91c33-192">On the **myPolicies Configuration** section, click **Configure myPolicies** to open **Configure sign-on** window.</span></span> <span data-ttu-id="91c33-193">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="91c33-193">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/mypolicies-tutorial/tutorial_mypolicies_configure.png) 

1. <span data-ttu-id="91c33-195">To configure single sign-on on **myPolicies** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [myPolicies support team](mailto:support@mypolicies.com).</span><span class="sxs-lookup"><span data-stu-id="91c33-195">To configure single sign-on on **myPolicies** side, you need to send the downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** to [myPolicies support team](mailto:support@mypolicies.com).</span></span> 

> [!TIP]
> <span data-ttu-id="91c33-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="91c33-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="91c33-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="91c33-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="91c33-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="91c33-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="91c33-199">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="91c33-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="91c33-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="91c33-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="91c33-202">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91c33-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="91c33-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="91c33-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/mypolicies-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="91c33-205">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="91c33-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/mypolicies-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="91c33-207">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="91c33-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/mypolicies-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="91c33-209">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="91c33-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/mypolicies-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="91c33-211">a.</span><span class="sxs-lookup"><span data-stu-id="91c33-211">a.</span></span> <span data-ttu-id="91c33-212">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="91c33-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="91c33-213">b.</span><span class="sxs-lookup"><span data-stu-id="91c33-213">b.</span></span> <span data-ttu-id="91c33-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="91c33-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="91c33-215">c.</span><span class="sxs-lookup"><span data-stu-id="91c33-215">c.</span></span> <span data-ttu-id="91c33-216">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="91c33-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="91c33-217">d.</span><span class="sxs-lookup"><span data-stu-id="91c33-217">d.</span></span> <span data-ttu-id="91c33-218">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="91c33-218">Click **Create**.</span></span>
 
### <a name="creating-a-mypolicies-test-user"></a><span data-ttu-id="91c33-219">Creating a myPolicies test user</span><span class="sxs-lookup"><span data-stu-id="91c33-219">Creating a myPolicies test user</span></span>

<span data-ttu-id="91c33-220">In this section, you create a user called Britta Simon in myPolicies.</span><span class="sxs-lookup"><span data-stu-id="91c33-220">In this section, you create a user called Britta Simon in myPolicies.</span></span> <span data-ttu-id="91c33-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add the users in the myPolicies platform.</span><span class="sxs-lookup"><span data-stu-id="91c33-221">Work with [myPolicies support team](mailto:support@mypolicies.com) to add the users in the myPolicies platform.</span></span> <span data-ttu-id="91c33-222">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="91c33-222">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="91c33-223">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="91c33-223">Assigning the Azure AD test user</span></span>

<span data-ttu-id="91c33-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to myPolicies.</span><span class="sxs-lookup"><span data-stu-id="91c33-224">In this section, you enable Britta Simon to use Azure single sign-on by granting access to myPolicies.</span></span>

![Assign User][200] 

<span data-ttu-id="91c33-226">**To assign Britta Simon to myPolicies, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="91c33-226">**To assign Britta Simon to myPolicies, perform the following steps:**</span></span>

1. <span data-ttu-id="91c33-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="91c33-227">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="91c33-229">In the applications list, select **myPolicies**.</span><span class="sxs-lookup"><span data-stu-id="91c33-229">In the applications list, select **myPolicies**.</span></span>

    ![Configure Single Sign-On](./media/mypolicies-tutorial/tutorial_mypolicies_app.png) 

1. <span data-ttu-id="91c33-231">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="91c33-231">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="91c33-233">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="91c33-233">Click **Add** button.</span></span> <span data-ttu-id="91c33-234">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="91c33-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="91c33-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="91c33-236">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="91c33-237">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="91c33-237">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="91c33-238">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="91c33-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="91c33-239">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="91c33-239">Testing single sign-on</span></span>

<span data-ttu-id="91c33-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="91c33-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="91c33-241">When you click the myPolicies tile in the Access Panel, you should get automatically signed-on to your myPolicies application.</span><span class="sxs-lookup"><span data-stu-id="91c33-241">When you click the myPolicies tile in the Access Panel, you should get automatically signed-on to your myPolicies application.</span></span>
<span data-ttu-id="91c33-242">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="91c33-242">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="91c33-243">Additional resources</span><span class="sxs-lookup"><span data-stu-id="91c33-243">Additional resources</span></span>

* [<span data-ttu-id="91c33-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="91c33-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="91c33-245">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="91c33-245">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/mypolicies-tutorial/tutorial_general_01.png
[2]: ./media/mypolicies-tutorial/tutorial_general_02.png
[3]: ./media/mypolicies-tutorial/tutorial_general_03.png
[4]: ./media/mypolicies-tutorial/tutorial_general_04.png

[100]: ./media/mypolicies-tutorial/tutorial_general_100.png

[200]: ./media/mypolicies-tutorial/tutorial_general_200.png
[201]: ./media/mypolicies-tutorial/tutorial_general_201.png
[202]: ./media/mypolicies-tutorial/tutorial_general_202.png
[203]: ./media/mypolicies-tutorial/tutorial_general_203.png

