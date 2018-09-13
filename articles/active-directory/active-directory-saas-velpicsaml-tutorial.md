---
title: 'Tutorial: Azure Active Directory integration with Velpic SAML | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Velpic SAML.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: f9a3f0b539599a439b662c6d766459922de5d669
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556617"
---
# <a name="tutorial-azure-active-directory-integration-with-velpic-saml"></a><span data-ttu-id="9e42e-103">Tutorial: Azure Active Directory integration with Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="9e42e-103">Tutorial: Azure Active Directory integration with Velpic SAML</span></span>

<span data-ttu-id="9e42e-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9e42e-104">In this tutorial, you learn how to integrate Velpic SAML with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9e42e-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="9e42e-105">Integrating Velpic SAML with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9e42e-106">You can control in Azure AD who has access to Velpic SAML</span><span class="sxs-lookup"><span data-stu-id="9e42e-106">You can control in Azure AD who has access to Velpic SAML</span></span>
- <span data-ttu-id="9e42e-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="9e42e-107">You can enable your users to automatically get signed-on to Velpic SAML (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9e42e-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="9e42e-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="9e42e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9e42e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e42e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9e42e-110">Prerequisites</span></span>

<span data-ttu-id="9e42e-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="9e42e-111">To configure Azure AD integration with Velpic SAML, you need the following items:</span></span>

- <span data-ttu-id="9e42e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="9e42e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9e42e-113">A Velpic SAML single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="9e42e-113">A Velpic SAML single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9e42e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="9e42e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9e42e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="9e42e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9e42e-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="9e42e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="9e42e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e42e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9e42e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="9e42e-118">Scenario description</span></span>
<span data-ttu-id="9e42e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="9e42e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9e42e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="9e42e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9e42e-121">Adding Velpic SAML from the gallery</span><span class="sxs-lookup"><span data-stu-id="9e42e-121">Adding Velpic SAML from the gallery</span></span>
2. <span data-ttu-id="9e42e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9e42e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-velpic-saml-from-the-gallery"></a><span data-ttu-id="9e42e-123">Adding Velpic SAML from the gallery</span><span class="sxs-lookup"><span data-stu-id="9e42e-123">Adding Velpic SAML from the gallery</span></span>
<span data-ttu-id="9e42e-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="9e42e-124">To configure the integration of Velpic SAML into Azure AD, you need to add Velpic SAML from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9e42e-125">**To add Velpic SAML from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e42e-125">**To add Velpic SAML from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9e42e-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9e42e-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9e42e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9e42e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="9e42e-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="9e42e-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="9e42e-133">In the search box, type **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-133">In the search box, type **Velpic SAML**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_search.png)

5. <span data-ttu-id="9e42e-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="9e42e-135">In the results panel, select **Velpic SAML**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9e42e-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9e42e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9e42e-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="9e42e-138">In this section, you configure and test Azure AD single sign-on with Velpic SAML based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9e42e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9e42e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Velpic SAML is to a user in Azure AD.</span></span> <span data-ttu-id="9e42e-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span><span class="sxs-lookup"><span data-stu-id="9e42e-140">In other words, a link relationship between an Azure AD user and the related user in Velpic SAML needs to be established.</span></span>

<span data-ttu-id="9e42e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="9e42e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Velpic SAML.</span></span>

<span data-ttu-id="9e42e-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="9e42e-142">To configure and test Azure AD single sign-on with Velpic SAML, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9e42e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="9e42e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9e42e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e42e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9e42e-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="9e42e-145">**[Creating a Velpic SAML test user](#creating-a-velpic-saml-test-user)** - to have a counterpart of Britta Simon in Velpic SAML that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="9e42e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="9e42e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9e42e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="9e42e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9e42e-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="9e42e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9e42e-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span><span class="sxs-lookup"><span data-stu-id="9e42e-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Velpic SAML application.</span></span>

<span data-ttu-id="9e42e-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e42e-150">**To configure Azure AD single sign-on with Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="9e42e-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-151">In the Azure Management portal, on the **Velpic SAML** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="9e42e-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="9e42e-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_samlbase.png)

3. <span data-ttu-id="9e42e-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span><span class="sxs-lookup"><span data-stu-id="9e42e-155">Enter the details in the **Velpic SAML Domain and URLs** section-</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_url.png)

    <span data-ttu-id="9e42e-157">a.</span><span class="sxs-lookup"><span data-stu-id="9e42e-157">a.</span></span> <span data-ttu-id="9e42e-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span><span class="sxs-lookup"><span data-stu-id="9e42e-158">In the **Sign-on URL** textbox, type the value as: `https://<sub-domain>.velpicsaml.net`</span></span>

    <span data-ttu-id="9e42e-159">b.</span><span class="sxs-lookup"><span data-stu-id="9e42e-159">b.</span></span> <span data-ttu-id="9e42e-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span><span class="sxs-lookup"><span data-stu-id="9e42e-160">In the **Identifier** textbox, paste the **‘Single sign on URL’** value `https://auth.velpic.com/saml/v2/<entity-id>/login`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9e42e-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span><span class="sxs-lookup"><span data-stu-id="9e42e-161">Please note that the Sign on URL will be provided by the Velpic SAML team and Identifier value will be available when you configure the SSO Plugin on Velpic SAML side.</span></span> <span data-ttu-id="9e42e-162">You need to copy that value from Velpic SAML application  page and paste it here.</span><span class="sxs-lookup"><span data-stu-id="9e42e-162">You need to copy that value from Velpic SAML application  page and paste it here.</span></span>

4. <span data-ttu-id="9e42e-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="9e42e-163">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_certificate.png) 

5. <span data-ttu-id="9e42e-165">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="9e42e-165">Click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9e42e-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span><span class="sxs-lookup"><span data-stu-id="9e42e-167">On the Velpic SAML Configuration section, click Configure Velpic SAML to open Configure sign-on window.</span></span> <span data-ttu-id="9e42e-168">Copy the SAML Entity ID from the Quick Reference section.</span><span class="sxs-lookup"><span data-stu-id="9e42e-168">Copy the SAML Entity ID from the Quick Reference section.</span></span>

7. <span data-ttu-id="9e42e-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="9e42e-169">In a different web browser window, log into your Velpic SAML company site as an administrator.</span></span>

8. <span data-ttu-id="9e42e-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span><span class="sxs-lookup"><span data-stu-id="9e42e-170">Click on **Manage** tab and go to **Integration** section where you need to click on **Plugins** button to create new plugin for Sign-In.</span></span>

    ![Plugin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/velpic_1.png)

9. <span data-ttu-id="9e42e-172">Click on the **‘Add plugin’** button.</span><span class="sxs-lookup"><span data-stu-id="9e42e-172">Click on the **‘Add plugin’** button.</span></span>
    
    ![Plugin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/velpic_2.png)

10. <span data-ttu-id="9e42e-174">Click on the **SAML** tile in the Add Plugin page.</span><span class="sxs-lookup"><span data-stu-id="9e42e-174">Click on the **SAML** tile in the Add Plugin page.</span></span>
    
    ![Plugin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/velpic_3.png)

11. <span data-ttu-id="9e42e-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span><span class="sxs-lookup"><span data-stu-id="9e42e-176">Enter the name of the new SAML plugin and click the **‘Add’** button.</span></span>

    ![Plugin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/velpic_4.png)

12. <span data-ttu-id="9e42e-178">Enter the details as follows:</span><span class="sxs-lookup"><span data-stu-id="9e42e-178">Enter the details as follows:</span></span>

    ![Plugin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/velpic_5.png)

    <span data-ttu-id="9e42e-180">a.</span><span class="sxs-lookup"><span data-stu-id="9e42e-180">a.</span></span> <span data-ttu-id="9e42e-181">In the **Name** textbox, type the name of SAML plugin.</span><span class="sxs-lookup"><span data-stu-id="9e42e-181">In the **Name** textbox, type the name of SAML plugin.</span></span>

    <span data-ttu-id="9e42e-182">b.</span><span class="sxs-lookup"><span data-stu-id="9e42e-182">b.</span></span> <span data-ttu-id="9e42e-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9e42e-183">In the **Issuer URL** textbox, paste the **SAML Entity ID** you copied from the **Configure sign-on** window of the Azure portal.</span></span>

    <span data-ttu-id="9e42e-184">c.</span><span class="sxs-lookup"><span data-stu-id="9e42e-184">c.</span></span> <span data-ttu-id="9e42e-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9e42e-185">In the **Provider Metadata Config** upload the Metadata XML file which you downloaded from Azure portal.</span></span>

    <span data-ttu-id="9e42e-186">d.</span><span class="sxs-lookup"><span data-stu-id="9e42e-186">d.</span></span> <span data-ttu-id="9e42e-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span><span class="sxs-lookup"><span data-stu-id="9e42e-187">You can also choose to enable SAML just in time provisioning by enabling the **‘Auto create new users’** checkbox.</span></span> <span data-ttu-id="9e42e-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span><span class="sxs-lookup"><span data-stu-id="9e42e-188">If a user doesn’t exist in Velpic and this flag is not enabled, the login from Azure will fail.</span></span> <span data-ttu-id="9e42e-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span><span class="sxs-lookup"><span data-stu-id="9e42e-189">If the flag is enabled the user will automatically be provisioned into Velpic at the time of login.</span></span> 

    <span data-ttu-id="9e42e-190">e.</span><span class="sxs-lookup"><span data-stu-id="9e42e-190">e.</span></span> <span data-ttu-id="9e42e-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9e42e-191">Copy the **Single sign on URL** from the text box and paste it in the Azure portal.</span></span>
    
    <span data-ttu-id="9e42e-192">f.</span><span class="sxs-lookup"><span data-stu-id="9e42e-192">f.</span></span> <span data-ttu-id="9e42e-193">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-193">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9e42e-194">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9e42e-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="9e42e-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e42e-195">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="9e42e-197">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e42e-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9e42e-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="9e42e-198">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9e42e-200">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="9e42e-200">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9e42e-202">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="9e42e-202">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9e42e-204">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="9e42e-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9e42e-206">a.</span><span class="sxs-lookup"><span data-stu-id="9e42e-206">a.</span></span> <span data-ttu-id="9e42e-207">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9e42e-208">b.</span><span class="sxs-lookup"><span data-stu-id="9e42e-208">b.</span></span> <span data-ttu-id="9e42e-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9e42e-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9e42e-210">c.</span><span class="sxs-lookup"><span data-stu-id="9e42e-210">c.</span></span> <span data-ttu-id="9e42e-211">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9e42e-212">d.</span><span class="sxs-lookup"><span data-stu-id="9e42e-212">d.</span></span> <span data-ttu-id="9e42e-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-213">Click **Create**.</span></span>
 
### <a name="creating-a-velpic-saml-test-user"></a><span data-ttu-id="9e42e-214">Creating a Velpic SAML test user</span><span class="sxs-lookup"><span data-stu-id="9e42e-214">Creating a Velpic SAML test user</span></span>

<span data-ttu-id="9e42e-215">This step is usually not required as the application supports just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="9e42e-215">This step is usually not required as the application supports just in time user provisioning.</span></span> <span data-ttu-id="9e42e-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span><span class="sxs-lookup"><span data-stu-id="9e42e-216">If the automatic user provisioning is not enabled then manual user creation can be done as described below.</span></span>

<span data-ttu-id="9e42e-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span><span class="sxs-lookup"><span data-stu-id="9e42e-217">Log into your Velpic SAML company site as an administrator and perform following steps:</span></span>
    
1. <span data-ttu-id="9e42e-218">Click on Manage tab and go to Users section, then click on New button to add users.</span><span class="sxs-lookup"><span data-stu-id="9e42e-218">Click on Manage tab and go to Users section, then click on New button to add users.</span></span>

    ![add user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/velpic_7.png)

2. <span data-ttu-id="9e42e-220">On the **“Create New User”** dialog page, perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="9e42e-220">On the **“Create New User”** dialog page, perform the following steps.</span></span>

    ![user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/velpic_8.png)
    
    <span data-ttu-id="9e42e-222">a.</span><span class="sxs-lookup"><span data-stu-id="9e42e-222">a.</span></span> <span data-ttu-id="9e42e-223">In the **First Name** textbox, type the first name of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e42e-223">In the **First Name** textbox, type the first name of Britta Simon.</span></span>

    <span data-ttu-id="9e42e-224">b.</span><span class="sxs-lookup"><span data-stu-id="9e42e-224">b.</span></span> <span data-ttu-id="9e42e-225">In the **Last Name** textbox, type the last name of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e42e-225">In the **Last Name** textbox, type the last name of Britta Simon.</span></span>

    <span data-ttu-id="9e42e-226">c.</span><span class="sxs-lookup"><span data-stu-id="9e42e-226">c.</span></span> <span data-ttu-id="9e42e-227">In the **User Name** textbox, type the user name of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9e42e-227">In the **User Name** textbox, type the user name of Britta Simon.</span></span>

    <span data-ttu-id="9e42e-228">d.</span><span class="sxs-lookup"><span data-stu-id="9e42e-228">d.</span></span> <span data-ttu-id="9e42e-229">In the **Email** textbox, type the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="9e42e-229">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="9e42e-230">e.</span><span class="sxs-lookup"><span data-stu-id="9e42e-230">e.</span></span> <span data-ttu-id="9e42e-231">Rest of the information is optional, you can fill it if needed.</span><span class="sxs-lookup"><span data-stu-id="9e42e-231">Rest of the information is optional, you can fill it if needed.</span></span>
    
    <span data-ttu-id="9e42e-232">f.</span><span class="sxs-lookup"><span data-stu-id="9e42e-232">f.</span></span> <span data-ttu-id="9e42e-233">Click **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-233">Click **SAVE**.</span></span>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9e42e-234">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="9e42e-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9e42e-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span><span class="sxs-lookup"><span data-stu-id="9e42e-235">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Velpic SAML.</span></span>

![Assign User][200] 

<span data-ttu-id="9e42e-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="9e42e-237">**To assign Britta Simon to Velpic SAML, perform the following steps:**</span></span>

1. <span data-ttu-id="9e42e-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-238">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="9e42e-240">In the applications list, select **Velpic SAML**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-240">In the applications list, select **Velpic SAML**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_velpicsaml_app.png) 

3. <span data-ttu-id="9e42e-242">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="9e42e-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="9e42e-244">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9e42e-244">Click **Add** button.</span></span> <span data-ttu-id="9e42e-245">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9e42e-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="9e42e-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="9e42e-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9e42e-248">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="9e42e-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9e42e-249">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="9e42e-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9e42e-250">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="9e42e-250">Testing single sign-on</span></span>

<span data-ttu-id="9e42e-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="9e42e-251">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="9e42e-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span><span class="sxs-lookup"><span data-stu-id="9e42e-252">When you click the Velpic SAML tile in the Access Panel, you should get login page of Velpic SAML application.</span></span> <span data-ttu-id="9e42e-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span><span class="sxs-lookup"><span data-stu-id="9e42e-253">You should see the **‘Log In With Azure AD’** button on the sign in page.</span></span>

    ![Plugin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/velpic_6.png)

2. <span data-ttu-id="9e42e-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="9e42e-255">Click on the **‘Log In With Azure AD’** button to log in to Velpic using your Azure AD account.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="9e42e-256">Additional resources</span><span class="sxs-lookup"><span data-stu-id="9e42e-256">Additional resources</span></span>

* [<span data-ttu-id="9e42e-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9e42e-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9e42e-258">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9e42e-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-velpicsaml-tutorial/tutorial_general_203.png





























