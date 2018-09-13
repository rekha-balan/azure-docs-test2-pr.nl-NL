---
title: 'Tutorial: Azure Active Directory integration with Softeon WMS | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Softeon WMS.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 07c5de0d-90aa-43b3-b24e-0cc334b2f9b0
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jeedes
ms.openlocfilehash: 158879a78fca70bd46e56fcd369e0ac494f79652
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864863"
---
# <a name="tutorial-azure-active-directory-integration-with-softeon-wms"></a><span data-ttu-id="d3619-103">Tutorial: Azure Active Directory integration with Softeon WMS</span><span class="sxs-lookup"><span data-stu-id="d3619-103">Tutorial: Azure Active Directory integration with Softeon WMS</span></span>

<span data-ttu-id="d3619-104">In this tutorial, you learn how to integrate Softeon WMS with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3619-104">In this tutorial, you learn how to integrate Softeon WMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3619-105">Integrating Softeon WMS with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d3619-105">Integrating Softeon WMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d3619-106">You can control in Azure AD who has access to Softeon WMS</span><span class="sxs-lookup"><span data-stu-id="d3619-106">You can control in Azure AD who has access to Softeon WMS</span></span>
- <span data-ttu-id="d3619-107">You can enable your users to automatically get signed-on to Softeon WMS (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d3619-107">You can enable your users to automatically get signed-on to Softeon WMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d3619-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d3619-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d3619-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d3619-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3619-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d3619-110">Prerequisites</span></span>

<span data-ttu-id="d3619-111">To configure Azure AD integration with Softeon WMS, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d3619-111">To configure Azure AD integration with Softeon WMS, you need the following items:</span></span>

- <span data-ttu-id="d3619-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d3619-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3619-113">A Softeon WMS single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d3619-113">A Softeon WMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3619-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d3619-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3619-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d3619-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3619-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d3619-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3619-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3619-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3619-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d3619-118">Scenario description</span></span>
<span data-ttu-id="d3619-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d3619-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3619-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d3619-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3619-121">Adding Softeon WMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="d3619-121">Adding Softeon WMS from the gallery</span></span>
1. <span data-ttu-id="d3619-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3619-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-softeon-wms-from-the-gallery"></a><span data-ttu-id="d3619-123">Adding Softeon WMS from the gallery</span><span class="sxs-lookup"><span data-stu-id="d3619-123">Adding Softeon WMS from the gallery</span></span>
<span data-ttu-id="d3619-124">To configure the integration of Softeon WMS into Azure AD, you need to add Softeon WMS from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d3619-124">To configure the integration of Softeon WMS into Azure AD, you need to add Softeon WMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3619-125">**To add Softeon WMS from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3619-125">**To add Softeon WMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3619-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d3619-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="d3619-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d3619-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d3619-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d3619-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="d3619-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d3619-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="d3619-133">In the search box, type **Softeon WMS**.</span><span class="sxs-lookup"><span data-stu-id="d3619-133">In the search box, type **Softeon WMS**.</span></span>

    ![Creating an Azure AD test user](./media/softeon-tutorial/tutorial_softeon_search.png)

1. <span data-ttu-id="d3619-135">In the results panel, select **Softeon WMS**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d3619-135">In the results panel, select **Softeon WMS**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/softeon-tutorial/tutorial_softeon_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d3619-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3619-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d3619-138">In this section, you configure and test Azure AD single sign-on with Softeon WMS based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="d3619-138">In this section, you configure and test Azure AD single sign-on with Softeon WMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d3619-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Softeon WMS is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3619-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Softeon WMS is to a user in Azure AD.</span></span> <span data-ttu-id="d3619-140">In other words, a link relationship between an Azure AD user and the related user in Softeon WMS needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d3619-140">In other words, a link relationship between an Azure AD user and the related user in Softeon WMS needs to be established.</span></span>

<span data-ttu-id="d3619-141">In Softeon WMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="d3619-141">In Softeon WMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d3619-142">To configure and test Azure AD single sign-on with Softeon WMS, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d3619-142">To configure and test Azure AD single sign-on with Softeon WMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3619-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d3619-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d3619-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3619-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d3619-145">**[Creating a Softeon WMS test user](#creating-a-softeon-wms-test-user)** - to have a counterpart of Britta Simon in Softeon WMS that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d3619-145">**[Creating a Softeon WMS test user](#creating-a-softeon-wms-test-user)** - to have a counterpart of Britta Simon in Softeon WMS that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d3619-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d3619-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d3619-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d3619-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d3619-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3619-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d3619-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Softeon WMS application.</span><span class="sxs-lookup"><span data-stu-id="d3619-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Softeon WMS application.</span></span>

<span data-ttu-id="d3619-150">**To configure Azure AD single sign-on with Softeon WMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3619-150">**To configure Azure AD single sign-on with Softeon WMS, perform the following steps:**</span></span>

1. <span data-ttu-id="d3619-151">In the Azure portal, on the **Softeon WMS** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d3619-151">In the Azure portal, on the **Softeon WMS** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="d3619-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d3619-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/softeon-tutorial/tutorial_softeon_samlbase.png)

1. <span data-ttu-id="d3619-155">On the **Softeon WMS Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d3619-155">On the **Softeon WMS Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/softeon-tutorial/tutorial_softeon_url.png)

    <span data-ttu-id="d3619-157">a.</span><span class="sxs-lookup"><span data-stu-id="d3619-157">a.</span></span> <span data-ttu-id="d3619-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.softeon.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="d3619-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.softeon.com/<instancename>`</span></span>

    <span data-ttu-id="d3619-159">b.</span><span class="sxs-lookup"><span data-stu-id="d3619-159">b.</span></span> <span data-ttu-id="d3619-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.softeon.com/sp`</span><span class="sxs-lookup"><span data-stu-id="d3619-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.softeon.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d3619-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="d3619-161">These values are not real.</span></span> <span data-ttu-id="d3619-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="d3619-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d3619-163">Contact [Softeon WMS Client support team](mailto:contact@softeon.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="d3619-163">Contact [Softeon WMS Client support team](mailto:contact@softeon.com) to get these values.</span></span> 
 
1. <span data-ttu-id="d3619-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d3619-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/softeon-tutorial/tutorial_softeon_certificate.png) 

1. <span data-ttu-id="d3619-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d3619-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/softeon-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="d3619-168">On the **Softeon WMS Configuration** section, click **Configure Softeon WMS** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="d3619-168">On the **Softeon WMS Configuration** section, click **Configure Softeon WMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d3619-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="d3619-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/softeon-tutorial/tutorial_softeon_configure.png) 

1. <span data-ttu-id="d3619-171">To configure single sign-on on **Softeon WMS** side, you need to send the downloaded **Certificate (Base64), SAML Entity ID, and SAML Single Sign-On Service URL** to [Softeon WMS support team](mailto:contact@softeon.com).</span><span class="sxs-lookup"><span data-stu-id="d3619-171">To configure single sign-on on **Softeon WMS** side, you need to send the downloaded **Certificate (Base64), SAML Entity ID, and SAML Single Sign-On Service URL** to [Softeon WMS support team](mailto:contact@softeon.com).</span></span> <span data-ttu-id="d3619-172">They set this setting to have the SAML SSO connection set properly on both sides.</span><span class="sxs-lookup"><span data-stu-id="d3619-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="d3619-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="d3619-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d3619-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d3619-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d3619-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d3619-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d3619-176">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d3619-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="d3619-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3619-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="d3619-179">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3619-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3619-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d3619-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/softeon-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="d3619-182">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d3619-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/softeon-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="d3619-184">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="d3619-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/softeon-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="d3619-186">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d3619-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/softeon-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d3619-188">a.</span><span class="sxs-lookup"><span data-stu-id="d3619-188">a.</span></span> <span data-ttu-id="d3619-189">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3619-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3619-190">b.</span><span class="sxs-lookup"><span data-stu-id="d3619-190">b.</span></span> <span data-ttu-id="d3619-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d3619-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d3619-192">c.</span><span class="sxs-lookup"><span data-stu-id="d3619-192">c.</span></span> <span data-ttu-id="d3619-193">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="d3619-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d3619-194">d.</span><span class="sxs-lookup"><span data-stu-id="d3619-194">d.</span></span> <span data-ttu-id="d3619-195">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d3619-195">Click **Create**.</span></span>
 
### <a name="creating-a-softeon-wms-test-user"></a><span data-ttu-id="d3619-196">Creating a Softeon WMS test user</span><span class="sxs-lookup"><span data-stu-id="d3619-196">Creating a Softeon WMS test user</span></span>

<span data-ttu-id="d3619-197">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="d3619-197">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d3619-198">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d3619-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d3619-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Softeon WMS.</span><span class="sxs-lookup"><span data-stu-id="d3619-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Softeon WMS.</span></span>

![Assign User][200] 

<span data-ttu-id="d3619-201">**To assign Britta Simon to Softeon WMS, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d3619-201">**To assign Britta Simon to Softeon WMS, perform the following steps:**</span></span>

1. <span data-ttu-id="d3619-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d3619-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d3619-204">In the applications list, select **Softeon WMS**.</span><span class="sxs-lookup"><span data-stu-id="d3619-204">In the applications list, select **Softeon WMS**.</span></span>

    ![Configure Single Sign-On](./media/softeon-tutorial/tutorial_softeon_app.png) 

1. <span data-ttu-id="d3619-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d3619-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="d3619-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d3619-208">Click **Add** button.</span></span> <span data-ttu-id="d3619-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d3619-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="d3619-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d3619-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d3619-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d3619-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d3619-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d3619-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d3619-214">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="d3619-214">Testing single sign-on</span></span>

<span data-ttu-id="d3619-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d3619-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d3619-216">When you click the Softeon WMS tile in the Access Panel, you should get login page of Softeon WMS application.</span><span class="sxs-lookup"><span data-stu-id="d3619-216">When you click the Softeon WMS tile in the Access Panel, you should get login page of Softeon WMS application.</span></span>
<span data-ttu-id="d3619-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d3619-217">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d3619-218">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d3619-218">Additional resources</span></span>

* [<span data-ttu-id="d3619-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3619-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d3619-220">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d3619-220">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/softeon-tutorial/tutorial_general_01.png
[2]: ./media/softeon-tutorial/tutorial_general_02.png
[3]: ./media/softeon-tutorial/tutorial_general_03.png
[4]: ./media/softeon-tutorial/tutorial_general_04.png

[100]: ./media/softeon-tutorial/tutorial_general_100.png

[200]: ./media/softeon-tutorial/tutorial_general_200.png
[201]: ./media/softeon-tutorial/tutorial_general_201.png
[202]: ./media/softeon-tutorial/tutorial_general_202.png
[203]: ./media/softeon-tutorial/tutorial_general_203.png

