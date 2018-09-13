---
title: 'Tutorial: Azure Active Directory integration with Velpic SAML | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Velpic SAML.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 2ca95f6fd94036e86aae2059c05a3fbb0380005e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969343"
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="6c614-103">Tutorial: Azure Active Directory integration with Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="6c614-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="6c614-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6c614-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c614-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="6c614-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6c614-106">You can control in Azure AD who has access to Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="6c614-106">You can control in Azure AD who has access to Velpic SAML</span></span>
- <span data-ttu-id="6c614-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="6c614-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6c614-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="6c614-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="6c614-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="6c614-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c614-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c614-110">Prerequisites</span></span>

<span data-ttu-id="6c614-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="6c614-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span></span>

- <span data-ttu-id="6c614-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="6c614-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c614-113">A Velpic SAML single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="6c614-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6c614-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="6c614-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6c614-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="6c614-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c614-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="6c614-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="6c614-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c614-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6c614-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="6c614-118">Scenario description</span></span>
<span data-ttu-id="6c614-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="6c614-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c614-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="6c614-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c614-121">Adding Velpic SAML from the gallery</span><span class="sxs-lookup"><span data-stu-id="6c614-121">Adding Velpic SAML from the gallery</span></span>
1. <span data-ttu-id="6c614-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c614-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-the-gallery"></a><span data-ttu-id="6c614-123">Adding Velpic SAML from the gallery</span><span class="sxs-lookup"><span data-stu-id="6c614-123">Adding Velpic SAML from the gallery</span></span>
<span data-ttu-id="6c614-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6c614-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6c614-125">**To add Velpic SAML from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c614-125">**To add Velpic SAML from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6c614-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6c614-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="6c614-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="6c614-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6c614-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6c614-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="6c614-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="6c614-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="6c614-133">In the search box, type **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="6c614-133">In the search box, type **Velpic SAML**.</span></span>

    ![Creating an Azure AD test user](./media/velpicsaml-tutorial/tutorial_velpicsaml_search.png)

1. <span data-ttu-id="6c614-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="6c614-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6c614-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c614-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6c614-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="6c614-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6c614-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c614-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span></span> <span data-ttu-id="6c614-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span><span class="sxs-lookup"><span data-stu-id="6c614-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span></span>

<span data-ttu-id="6c614-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="6c614-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span></span>

<span data-ttu-id="6c614-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="6c614-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6c614-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="6c614-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="6c614-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c614-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="6c614-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="6c614-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span></span>
1. <span data-ttu-id="6c614-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="6c614-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="6c614-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="6c614-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6c614-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c614-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6c614-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span><span class="sxs-lookup"><span data-stu-id="6c614-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="6c614-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c614-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="6c614-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="6c614-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="6c614-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="6c614-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](./media/velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

1. <span data-ttu-id="6c614-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span><span class="sxs-lookup"><span data-stu-id="6c614-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span></span>

    ![Configure Single Sign-On](./media/velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="6c614-157">a.</span><span class="sxs-lookup"><span data-stu-id="6c614-157">a.</span></span> <span data-ttu-id="6c614-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="6c614-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="6c614-159">b.</span><span class="sxs-lookup"><span data-stu-id="6c614-159">b.</span></span> <span data-ttu-id="6c614-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="6c614-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="6c614-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span><span class="sxs-lookup"><span data-stu-id="6c614-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="6c614-162">You need to copy that value from Velpic SAML application  page and paste it here.</span><span class="sxs-lookup"><span data-stu-id="6c614-162">You need to copy that value from Velpic SAML application  page and paste it here.</span></span>

1. <span data-ttu-id="6c614-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="6c614-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

1. <span data-ttu-id="6c614-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="6c614-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/velpicsaml-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="6c614-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span><span class="sxs-lookup"><span data-stu-id="6c614-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span></span> <span data-ttu-id="6c614-168">Copy the SAML Entity ID from the Quick Reference section.</span><span class="sxs-lookup"><span data-stu-id="6c614-168">Copy the SAML Entity ID from the Quick Reference section.</span></span>

1. <span data-ttu-id="6c614-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="6c614-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

1. <span data-ttu-id="6c614-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span><span class="sxs-lookup"><span data-stu-id="6c614-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span></span>

    ![Plugin](./media/velpicsaml-tutorial/velpic_1.png)

1. <span data-ttu-id="6c614-172">Click on the **‘Add plugin’** button.</span><span class="sxs-lookup"><span data-stu-id="6c614-172">Click on the **‘Add plugin’** button.</span></span>
    
    ![Plugin](./media/velpicsaml-tutorial/velpic_2.png)

1. <span data-ttu-id="6c614-174">Click on the **SAML** tile in the Add Plugin page.</span><span class="sxs-lookup"><span data-stu-id="6c614-174">Click on the **SAML** tile in the Add Plugin page.</span></span>
    
    ![Plugin](./media/velpicsaml-tutorial/velpic_3.png)

1. <span data-ttu-id="6c614-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span><span class="sxs-lookup"><span data-stu-id="6c614-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span></span>

    ![Plugin](./media/velpicsaml-tutorial/velpic_4.png)

1. <span data-ttu-id="6c614-178">Enter the details as follows:</span><span class="sxs-lookup"><span data-stu-id="6c614-178">Enter the details as follows:</span></span>

    ![Plugin](./media/velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="6c614-180">a.</span><span class="sxs-lookup"><span data-stu-id="6c614-180">a.</span></span> <span data-ttu-id="6c614-181">In the **Name** textbox, type the name of SAML plugin.</span><span class="sxs-lookup"><span data-stu-id="6c614-181">In the **Name** textbox, type the name of SAML plugin.</span></span>

    <span data-ttu-id="6c614-182">b.</span><span class="sxs-lookup"><span data-stu-id="6c614-182">b.</span></span> <span data-ttu-id="6c614-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6c614-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="6c614-184">c.</span><span class="sxs-lookup"><span data-stu-id="6c614-184">c.</span></span> <span data-ttu-id="6c614-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6c614-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="6c614-186">d.</span><span class="sxs-lookup"><span data-stu-id="6c614-186">d.</span></span> <span data-ttu-id="6c614-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span><span class="sxs-lookup"><span data-stu-id="6c614-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="6c614-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span><span class="sxs-lookup"><span data-stu-id="6c614-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span></span> <span data-ttu-id="6c614-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span><span class="sxs-lookup"><span data-stu-id="6c614-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span></span> 

    <span data-ttu-id="6c614-190">e.</span><span class="sxs-lookup"><span data-stu-id="6c614-190">e.</span></span> <span data-ttu-id="6c614-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6c614-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span></span>
    
    <span data-ttu-id="6c614-192">f.</span><span class="sxs-lookup"><span data-stu-id="6c614-192">f.</span></span> <span data-ttu-id="6c614-193">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6c614-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6c614-194">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6c614-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="6c614-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c614-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="6c614-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c614-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6c614-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="6c614-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/velpicsaml-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="6c614-200">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="6c614-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](./media/velpicsaml-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="6c614-202">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="6c614-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/velpicsaml-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="6c614-204">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c614-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6c614-206">a.</span><span class="sxs-lookup"><span data-stu-id="6c614-206">a.</span></span> <span data-ttu-id="6c614-207">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6c614-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6c614-208">b.</span><span class="sxs-lookup"><span data-stu-id="6c614-208">b.</span></span> <span data-ttu-id="6c614-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6c614-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6c614-210">c.</span><span class="sxs-lookup"><span data-stu-id="6c614-210">c.</span></span> <span data-ttu-id="6c614-211">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="6c614-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6c614-212">d.</span><span class="sxs-lookup"><span data-stu-id="6c614-212">d.</span></span> <span data-ttu-id="6c614-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6c614-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="6c614-214">Creating a Velpic SAML test user</span><span class="sxs-lookup"><span data-stu-id="6c614-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="6c614-215">This step is usually not required as the application supports just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="6c614-215">This step is usually not required as the application supports just in time user provisioning.</span></span> <span data-ttu-id="6c614-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span><span class="sxs-lookup"><span data-stu-id="6c614-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="6c614-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span><span class="sxs-lookup"><span data-stu-id="6c614-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="6c614-218">Click on Manage tab and go to Users section, then click on New button to add users.</span><span class="sxs-lookup"><span data-stu-id="6c614-218">Click on Manage tab and go to Users section, then click on New button to add users.</span></span>

    ![add user](./media/velpicsaml-tutorial/velpic_7.png)

1. <span data-ttu-id="6c614-220">On the **“Create New User”** dialog page, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="6c614-220">On the **“Create New User”** dialog page, perform the following steps.</span></span>

    ![user](./media/velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="6c614-222">a.</span><span class="sxs-lookup"><span data-stu-id="6c614-222">a.</span></span> <span data-ttu-id="6c614-223">In the **First Name** textbox, type the first name of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c614-223">In the **First Name** textbox, type the first name of Britta Simon.</span></span>

    <span data-ttu-id="6c614-224">b.</span><span class="sxs-lookup"><span data-stu-id="6c614-224">b.</span></span> <span data-ttu-id="6c614-225">In the **Last Name** textbox, type the last name of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c614-225">In the **Last Name** textbox, type the last name of Britta Simon.</span></span>

    <span data-ttu-id="6c614-226">c.</span><span class="sxs-lookup"><span data-stu-id="6c614-226">c.</span></span> <span data-ttu-id="6c614-227">In the **User Name** textbox, type the user name of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6c614-227">In the **User Name** textbox, type the user name of Britta Simon.</span></span>

    <span data-ttu-id="6c614-228">d.</span><span class="sxs-lookup"><span data-stu-id="6c614-228">d.</span></span> <span data-ttu-id="6c614-229">In the **Email** textbox, type the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="6c614-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="6c614-230">e.</span><span class="sxs-lookup"><span data-stu-id="6c614-230">e.</span></span> <span data-ttu-id="6c614-231">Rest of the information is optional, you can fill it if needed.</span><span class="sxs-lookup"><span data-stu-id="6c614-231">Rest of the information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="6c614-232">f.</span><span class="sxs-lookup"><span data-stu-id="6c614-232">f.</span></span> <span data-ttu-id="6c614-233">Click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="6c614-233">Click **SAVE**.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6c614-234">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="6c614-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6c614-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="6c614-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span></span>

![Assign User][200] 

<span data-ttu-id="6c614-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="6c614-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="6c614-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="6c614-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="6c614-240">In the applications list, select **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="6c614-240">In the applications list, select **Velpic SAML**.</span></span>

    ![Configure Single Sign-On](./media/velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

1. <span data-ttu-id="6c614-242">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="6c614-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="6c614-244">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="6c614-244">Click **Add** button.</span></span> <span data-ttu-id="6c614-245">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6c614-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="6c614-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="6c614-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="6c614-248">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="6c614-248">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="6c614-249">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="6c614-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6c614-250">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="6c614-250">Testing single sign-on</span></span>

<span data-ttu-id="6c614-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="6c614-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="6c614-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span><span class="sxs-lookup"><span data-stu-id="6c614-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="6c614-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span><span class="sxs-lookup"><span data-stu-id="6c614-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span></span>

    ![Plugin](./media/velpicsaml-tutorial/velpic_6.png)

1. <span data-ttu-id="6c614-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="6c614-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="6c614-256">Additional resources</span><span class="sxs-lookup"><span data-stu-id="6c614-256">Additional resources</span></span>

* [<span data-ttu-id="6c614-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c614-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="6c614-258">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6c614-258">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/velpicsaml-tutorial/tutorial_general_01.png
[2]: ./media/velpicsaml-tutorial/tutorial_general_02.png
[3]: ./media/velpicsaml-tutorial/tutorial_general_03.png
[4]: ./media/velpicsaml-tutorial/tutorial_general_04.png

[100]: ./media/velpicsaml-tutorial/tutorial_general_100.png

[200]: ./media/velpicsaml-tutorial/tutorial_general_200.png
[201]: ./media/velpicsaml-tutorial/tutorial_general_201.png
[202]: ./media/velpicsaml-tutorial/tutorial_general_202.png
[203]: ./media/velpicsaml-tutorial/tutorial_general_203.png

