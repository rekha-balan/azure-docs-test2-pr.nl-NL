---
title: 'Tutorial: Azure Active Directory integration with Reward Gateway | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Reward Gateway.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 34336386-998a-4d47-ab55-721d97708e5e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: d5cda8830b480e9ef9dff18cb3d7b99e1db55590
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857251"
---
# <a name="tutorial-azure-active-directory-integration-with-reward-gateway"></a><span data-ttu-id="d0afc-103">Tutorial: Azure Active Directory integration with Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="d0afc-103">Tutorial: Azure Active Directory integration with Reward Gateway</span></span>

<span data-ttu-id="d0afc-104">In this tutorial, you learn how to integrate Reward Gateway with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d0afc-104">In this tutorial, you learn how to integrate Reward Gateway with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d0afc-105">Integrating Reward Gateway with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d0afc-105">Integrating Reward Gateway with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d0afc-106">You can control in Azure AD who has access to Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="d0afc-106">You can control in Azure AD who has access to Reward Gateway</span></span>
- <span data-ttu-id="d0afc-107">You can enable your users to automatically get signed-on to Reward Gateway (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d0afc-107">You can enable your users to automatically get signed-on to Reward Gateway (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d0afc-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d0afc-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d0afc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d0afc-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0afc-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d0afc-110">Prerequisites</span></span>

<span data-ttu-id="d0afc-111">To configure Azure AD integration with Reward Gateway, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d0afc-111">To configure Azure AD integration with Reward Gateway, you need the following items:</span></span>

- <span data-ttu-id="d0afc-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d0afc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d0afc-113">A Reward Gateway single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d0afc-113">A Reward Gateway single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d0afc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d0afc-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d0afc-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d0afc-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d0afc-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d0afc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d0afc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d0afc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d0afc-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d0afc-118">Scenario description</span></span>
<span data-ttu-id="d0afc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d0afc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d0afc-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d0afc-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d0afc-121">Adding Reward Gateway from the gallery</span><span class="sxs-lookup"><span data-stu-id="d0afc-121">Adding Reward Gateway from the gallery</span></span>
1. <span data-ttu-id="d0afc-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d0afc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-reward-gateway-from-the-gallery"></a><span data-ttu-id="d0afc-123">Adding Reward Gateway from the gallery</span><span class="sxs-lookup"><span data-stu-id="d0afc-123">Adding Reward Gateway from the gallery</span></span>
<span data-ttu-id="d0afc-124">To configure the integration of Reward Gateway into Azure AD, you need to add Reward Gateway from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d0afc-124">To configure the integration of Reward Gateway into Azure AD, you need to add Reward Gateway from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d0afc-125">**To add Reward Gateway from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0afc-125">**To add Reward Gateway from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d0afc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d0afc-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="d0afc-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d0afc-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d0afc-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d0afc-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="d0afc-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d0afc-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="d0afc-133">In the search box, type **Reward Gateway**.</span><span class="sxs-lookup"><span data-stu-id="d0afc-133">In the search box, type **Reward Gateway**.</span></span>

    ![Creating an Azure AD test user](./media/reward-gateway-tutorial/tutorial_rewardgateway_search.png)

1. <span data-ttu-id="d0afc-135">In the results panel, select **Reward Gateway**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d0afc-135">In the results panel, select **Reward Gateway**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/reward-gateway-tutorial/tutorial_rewardgateway_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d0afc-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d0afc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d0afc-138">In this section, you configure and test Azure AD single sign-on with Reward Gateway based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d0afc-138">In this section, you configure and test Azure AD single sign-on with Reward Gateway based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d0afc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Reward Gateway is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d0afc-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Reward Gateway is to a user in Azure AD.</span></span> <span data-ttu-id="d0afc-140">In other words, a link relationship between an Azure AD user and the related user in Reward Gateway needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d0afc-140">In other words, a link relationship between an Azure AD user and the related user in Reward Gateway needs to be established.</span></span>

<span data-ttu-id="d0afc-141">In Reward Gateway, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="d0afc-141">In Reward Gateway, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d0afc-142">To configure and test Azure AD single sign-on with Reward Gateway, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d0afc-142">To configure and test Azure AD single sign-on with Reward Gateway, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d0afc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d0afc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d0afc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0afc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d0afc-145">**[Creating a Reward Gateway test user](#creating-a-reward-gateway-test-user)** - to have a counterpart of Britta Simon in Reward Gateway that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d0afc-145">**[Creating a Reward Gateway test user](#creating-a-reward-gateway-test-user)** - to have a counterpart of Britta Simon in Reward Gateway that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d0afc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d0afc-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d0afc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d0afc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d0afc-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d0afc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d0afc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Reward Gateway application.</span><span class="sxs-lookup"><span data-stu-id="d0afc-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Reward Gateway application.</span></span>

<span data-ttu-id="d0afc-150">**To configure Azure AD single sign-on with Reward Gateway, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0afc-150">**To configure Azure AD single sign-on with Reward Gateway, perform the following steps:**</span></span>

1. <span data-ttu-id="d0afc-151">In the Azure portal, on the **Reward Gateway** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d0afc-151">In the Azure portal, on the **Reward Gateway** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="d0afc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d0afc-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/reward-gateway-tutorial/tutorial_rewardgateway_samlbase.png)

1. <span data-ttu-id="d0afc-155">On the **Reward Gateway Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d0afc-155">On the **Reward Gateway Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/reward-gateway-tutorial/tutorial_rewardgateway_url.png)

    <span data-ttu-id="d0afc-157">a.</span><span class="sxs-lookup"><span data-stu-id="d0afc-157">a.</span></span> <span data-ttu-id="d0afc-158">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="d0afc-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.rewardgateway.com` |
    | `https://<companyname>.rewardgateway.co.uk/` |
    | `https://<companyname>.rewardgateway.co.nz/` |
    | `https://<companyname>.rewardgateway.com.au/` |

    <span data-ttu-id="d0afc-159">b.</span><span class="sxs-lookup"><span data-stu-id="d0afc-159">b.</span></span> <span data-ttu-id="d0afc-160">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="d0afc-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    |  `https://<companyname>.rewardgateway.com/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.uk/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.nz/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.com.au/Authentication/EndLogin?idp=<Unique Id>` |

    > [!NOTE] 
    > <span data-ttu-id="d0afc-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="d0afc-161">These values are not real.</span></span> <span data-ttu-id="d0afc-162">Update these values with the actual Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="d0afc-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="d0afc-163">To get these values start setting up an Integration on the Reward Manager Portal.</span><span class="sxs-lookup"><span data-stu-id="d0afc-163">To get these values start setting up an Integration on the Reward Manager Portal.</span></span> <span data-ttu-id="d0afc-164">Details can be found on http://success.rewardgateway.com/it-implementation/293968-how-to-configure-a-sso-integration</span><span class="sxs-lookup"><span data-stu-id="d0afc-164">Details can be found on http://success.rewardgateway.com/it-implementation/293968-how-to-configure-a-sso-integration</span></span>
 
1. <span data-ttu-id="d0afc-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d0afc-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/reward-gateway-tutorial/tutorial_rewardgateway_certificate.png) 

1. <span data-ttu-id="d0afc-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d0afc-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/reward-gateway-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="d0afc-169">To configure single sign-on on **Reward Gateway** side, start setting up an Integration on the Reward Manager Portal.</span><span class="sxs-lookup"><span data-stu-id="d0afc-169">To configure single sign-on on **Reward Gateway** side, start setting up an Integration on the Reward Manager Portal.</span></span> <span data-ttu-id="d0afc-170">Use the downloaded metadata to obtain your Signing Certificate and upload that during the configuration.</span><span class="sxs-lookup"><span data-stu-id="d0afc-170">Use the downloaded metadata to obtain your Signing Certificate and upload that during the configuration.</span></span> <span data-ttu-id="d0afc-171">Details can be found on http://success.rewardgateway.com/it-implementation/293968-how-to-configure-a-sso-integration</span><span class="sxs-lookup"><span data-stu-id="d0afc-171">Details can be found on http://success.rewardgateway.com/it-implementation/293968-how-to-configure-a-sso-integration</span></span>

> [!TIP]
> <span data-ttu-id="d0afc-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="d0afc-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d0afc-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d0afc-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d0afc-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d0afc-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d0afc-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d0afc-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="d0afc-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d0afc-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="d0afc-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0afc-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d0afc-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d0afc-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/reward-gateway-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="d0afc-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d0afc-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/reward-gateway-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="d0afc-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="d0afc-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/reward-gateway-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="d0afc-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d0afc-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/reward-gateway-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d0afc-187">a.</span><span class="sxs-lookup"><span data-stu-id="d0afc-187">a.</span></span> <span data-ttu-id="d0afc-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d0afc-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d0afc-189">b.</span><span class="sxs-lookup"><span data-stu-id="d0afc-189">b.</span></span> <span data-ttu-id="d0afc-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d0afc-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d0afc-191">c.</span><span class="sxs-lookup"><span data-stu-id="d0afc-191">c.</span></span> <span data-ttu-id="d0afc-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="d0afc-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d0afc-193">d.</span><span class="sxs-lookup"><span data-stu-id="d0afc-193">d.</span></span> <span data-ttu-id="d0afc-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d0afc-194">Click **Create**.</span></span>
 
### <a name="creating-a-reward-gateway-test-user"></a><span data-ttu-id="d0afc-195">Creating a Reward Gateway test user</span><span class="sxs-lookup"><span data-stu-id="d0afc-195">Creating a Reward Gateway test user</span></span>

<span data-ttu-id="d0afc-196">In this section, you create a user called Britta Simon in Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="d0afc-196">In this section, you create a user called Britta Simon in Reward Gateway.</span></span> <span data-ttu-id="d0afc-197">Work with Reward Gateway [support team](mailto:clientsupport@rewardgateway.com) to add the users in the Reward Gateway platform.</span><span class="sxs-lookup"><span data-stu-id="d0afc-197">Work with Reward Gateway [support team](mailto:clientsupport@rewardgateway.com) to add the users in the Reward Gateway platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d0afc-198">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d0afc-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d0afc-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="d0afc-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Reward Gateway.</span></span>

![Assign User][200] 

<span data-ttu-id="d0afc-201">**To assign Britta Simon to Reward Gateway, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d0afc-201">**To assign Britta Simon to Reward Gateway, perform the following steps:**</span></span>

1. <span data-ttu-id="d0afc-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d0afc-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d0afc-204">In the applications list, select **Reward Gateway**.</span><span class="sxs-lookup"><span data-stu-id="d0afc-204">In the applications list, select **Reward Gateway**.</span></span>

    ![Configure Single Sign-On](./media/reward-gateway-tutorial/tutorial_rewardgateway_app.png) 

1. <span data-ttu-id="d0afc-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d0afc-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="d0afc-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d0afc-208">Click **Add** button.</span></span> <span data-ttu-id="d0afc-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d0afc-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="d0afc-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d0afc-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d0afc-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d0afc-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d0afc-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d0afc-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d0afc-214">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="d0afc-214">Testing single sign-on</span></span>

<span data-ttu-id="d0afc-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d0afc-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d0afc-216">When you click the Reward Gateway tile in the Access Panel, you should get automatically signed-on to your Reward Gateway application.</span><span class="sxs-lookup"><span data-stu-id="d0afc-216">When you click the Reward Gateway tile in the Access Panel, you should get automatically signed-on to your Reward Gateway application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d0afc-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d0afc-217">Additional resources</span></span>

* [<span data-ttu-id="d0afc-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d0afc-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d0afc-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d0afc-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/reward-gateway-tutorial/tutorial_general_01.png
[2]: ./media/reward-gateway-tutorial/tutorial_general_02.png
[3]: ./media/reward-gateway-tutorial/tutorial_general_03.png
[4]: ./media/reward-gateway-tutorial/tutorial_general_04.png

[100]: ./media/reward-gateway-tutorial/tutorial_general_100.png

[200]: ./media/reward-gateway-tutorial/tutorial_general_200.png
[201]: ./media/reward-gateway-tutorial/tutorial_general_201.png
[202]: ./media/reward-gateway-tutorial/tutorial_general_202.png
[203]: ./media/reward-gateway-tutorial/tutorial_general_203.png

