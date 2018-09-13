---
title: 'Tutorial: Azure Active Directory integration with Zscaler | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Zscaler.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 68ddeefd9cbfadb3081885819506b6e916d03354
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871319"
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="55f1e-103">Tutorial: Azure Active Directory integration with Zscaler</span><span class="sxs-lookup"><span data-stu-id="55f1e-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>

<span data-ttu-id="55f1e-104">In this tutorial, you learn how to integrate Zscaler with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="55f1e-104">In this tutorial, you learn how to integrate Zscaler with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="55f1e-105">Integrating Zscaler with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="55f1e-105">Integrating Zscaler with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="55f1e-106">You can control in Azure AD who has access to Zscaler</span><span class="sxs-lookup"><span data-stu-id="55f1e-106">You can control in Azure AD who has access to Zscaler</span></span>
- <span data-ttu-id="55f1e-107">You can enable your users to automatically get signed-on to Zscaler (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="55f1e-107">You can enable your users to automatically get signed-on to Zscaler (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="55f1e-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="55f1e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="55f1e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="55f1e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="55f1e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="55f1e-110">Prerequisites</span></span>

<span data-ttu-id="55f1e-111">To configure Azure AD integration with Zscaler, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="55f1e-111">To configure Azure AD integration with Zscaler, you need the following items:</span></span>

- <span data-ttu-id="55f1e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="55f1e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="55f1e-113">A Zscaler single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="55f1e-113">A Zscaler single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="55f1e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="55f1e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="55f1e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="55f1e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="55f1e-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="55f1e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="55f1e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="55f1e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="55f1e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="55f1e-118">Scenario description</span></span>
<span data-ttu-id="55f1e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="55f1e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="55f1e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="55f1e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="55f1e-121">Adding Zscaler from the gallery</span><span class="sxs-lookup"><span data-stu-id="55f1e-121">Adding Zscaler from the gallery</span></span>
1. <span data-ttu-id="55f1e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="55f1e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-from-the-gallery"></a><span data-ttu-id="55f1e-123">Adding Zscaler from the gallery</span><span class="sxs-lookup"><span data-stu-id="55f1e-123">Adding Zscaler from the gallery</span></span>
<span data-ttu-id="55f1e-124">To configure the integration of Zscaler into Azure AD, you need to add Zscaler from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="55f1e-124">To configure the integration of Zscaler into Azure AD, you need to add Zscaler from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="55f1e-125">**To add Zscaler from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55f1e-125">**To add Zscaler from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="55f1e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="55f1e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="55f1e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="55f1e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="55f1e-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="55f1e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="55f1e-133">In the search box, type **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-133">In the search box, type **Zscaler**.</span></span>

    ![Creating an Azure AD test user](./media/zscaler-tutorial/tutorial_zscaler_search.png)

1. <span data-ttu-id="55f1e-135">In the results panel, select **Zscaler**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="55f1e-135">In the results panel, select **Zscaler**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="55f1e-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="55f1e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="55f1e-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="55f1e-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="55f1e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="55f1e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler is to a user in Azure AD.</span></span> <span data-ttu-id="55f1e-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler needs to be established.</span><span class="sxs-lookup"><span data-stu-id="55f1e-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler needs to be established.</span></span>

<span data-ttu-id="55f1e-141">In Zscaler, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="55f1e-141">In Zscaler, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="55f1e-142">To configure and test Azure AD single sign-on with Zscaler, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="55f1e-142">To configure and test Azure AD single sign-on with Zscaler, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="55f1e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="55f1e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="55f1e-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="55f1e-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
1. <span data-ttu-id="55f1e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55f1e-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="55f1e-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - to have a counterpart of Britta Simon in Zscaler that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="55f1e-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - to have a counterpart of Britta Simon in Zscaler that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="55f1e-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="55f1e-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="55f1e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="55f1e-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="55f1e-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="55f1e-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="55f1e-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler application.</span><span class="sxs-lookup"><span data-stu-id="55f1e-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler application.</span></span>

<span data-ttu-id="55f1e-151">**To configure Azure AD single sign-on with Zscaler, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55f1e-151">**To configure Azure AD single sign-on with Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="55f1e-152">In the Azure portal, on the **Zscaler** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-152">In the Azure portal, on the **Zscaler** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="55f1e-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="55f1e-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/zscaler-tutorial/tutorial_zscaler_samlbase.png)

1. <span data-ttu-id="55f1e-156">On the **Zscaler Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="55f1e-156">On the **Zscaler Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/zscaler-tutorial/tutorial_zscaler_url.png)

    <span data-ttu-id="55f1e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zsclaer.net`</span><span class="sxs-lookup"><span data-stu-id="55f1e-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zsclaer.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="55f1e-159">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="55f1e-159">This value is not real.</span></span> <span data-ttu-id="55f1e-160">Update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="55f1e-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="55f1e-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) to get this value.</span><span class="sxs-lookup"><span data-stu-id="55f1e-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) to get this value.</span></span> 

1. <span data-ttu-id="55f1e-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="55f1e-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/zscaler-tutorial/tutorial_zscaler_certificate.png) 

1. <span data-ttu-id="55f1e-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="55f1e-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/zscaler-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="55f1e-166">On the **Zscaler Configuration** section, click **Configure Zscaler** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="55f1e-166">On the **Zscaler Configuration** section, click **Configure Zscaler** to open **Configure sign-on** window.</span></span> <span data-ttu-id="55f1e-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="55f1e-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/zscaler-tutorial/tutorial_zscaler_configure.png) 

1. <span data-ttu-id="55f1e-169">In a different web browser window, log in to your ZScaler company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="55f1e-169">In a different web browser window, log in to your ZScaler company site as an administrator.</span></span>

1. <span data-ttu-id="55f1e-170">In the menu on the top, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-170">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="55f1e-171">![Administration](./media/zscaler-tutorial/ic800206.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="55f1e-171">![Administration](./media/zscaler-tutorial/ic800206.png "Administration")</span></span>

1. <span data-ttu-id="55f1e-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="55f1e-173">![Manage Users & Authentication](./media/zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span><span class="sxs-lookup"><span data-stu-id="55f1e-173">![Manage Users & Authentication](./media/zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

1. <span data-ttu-id="55f1e-174">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="55f1e-174">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="55f1e-175">![Authentication](./media/zscaler-tutorial/ic800208.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="55f1e-175">![Authentication](./media/zscaler-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="55f1e-176">a.</span><span class="sxs-lookup"><span data-stu-id="55f1e-176">a.</span></span> <span data-ttu-id="55f1e-177">Select **Authenticate using SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-177">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="55f1e-178">b.</span><span class="sxs-lookup"><span data-stu-id="55f1e-178">b.</span></span> <span data-ttu-id="55f1e-179">Click **Configure SAML Single Sign-On Parameters**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-179">Click **Configure SAML Single Sign-On Parameters**.</span></span>

1. <span data-ttu-id="55f1e-180">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span><span class="sxs-lookup"><span data-stu-id="55f1e-180">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="55f1e-181">![Single Sign-On](./media/zscaler-tutorial/ic800209.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="55f1e-181">![Single Sign-On](./media/zscaler-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="55f1e-182">a.</span><span class="sxs-lookup"><span data-stu-id="55f1e-182">a.</span></span> <span data-ttu-id="55f1e-183">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span><span class="sxs-lookup"><span data-stu-id="55f1e-183">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="55f1e-184">b.</span><span class="sxs-lookup"><span data-stu-id="55f1e-184">b.</span></span> <span data-ttu-id="55f1e-185">In the **Attribute containing Login Name** textbox, type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-185">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="55f1e-186">c.</span><span class="sxs-lookup"><span data-stu-id="55f1e-186">c.</span></span> <span data-ttu-id="55f1e-187">To upload your downloaded certificate, click **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-187">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="55f1e-188">d.</span><span class="sxs-lookup"><span data-stu-id="55f1e-188">d.</span></span> <span data-ttu-id="55f1e-189">Select **Enable SAML Auto-Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-189">Select **Enable SAML Auto-Provisioning**.</span></span>

1. <span data-ttu-id="55f1e-190">On the **Configure User Authentication** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="55f1e-190">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="55f1e-191">![Administration](./media/zscaler-tutorial/ic800210.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="55f1e-191">![Administration](./media/zscaler-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="55f1e-192">a.</span><span class="sxs-lookup"><span data-stu-id="55f1e-192">a.</span></span> <span data-ttu-id="55f1e-193">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-193">Click **Save**.</span></span>

    <span data-ttu-id="55f1e-194">b.</span><span class="sxs-lookup"><span data-stu-id="55f1e-194">b.</span></span> <span data-ttu-id="55f1e-195">Click **Activate Now**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-195">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="55f1e-196">Configuring proxy settings</span><span class="sxs-lookup"><span data-stu-id="55f1e-196">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="55f1e-197">To configure the proxy settings in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="55f1e-197">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="55f1e-198">Start **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-198">Start **Internet Explorer**.</span></span>

1. <span data-ttu-id="55f1e-199">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span><span class="sxs-lookup"><span data-stu-id="55f1e-199">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="55f1e-200">![Internet Options](./media/zscaler-tutorial/ic769492.png "Internet Options")</span><span class="sxs-lookup"><span data-stu-id="55f1e-200">![Internet Options](./media/zscaler-tutorial/ic769492.png "Internet Options")</span></span>

1. <span data-ttu-id="55f1e-201">Click the **Connections** tab.</span><span class="sxs-lookup"><span data-stu-id="55f1e-201">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="55f1e-202">![Connections](./media/zscaler-tutorial/ic769493.png "Connections")</span><span class="sxs-lookup"><span data-stu-id="55f1e-202">![Connections](./media/zscaler-tutorial/ic769493.png "Connections")</span></span>

1. <span data-ttu-id="55f1e-203">Click **LAN settings** to open the **LAN Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="55f1e-203">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

1. <span data-ttu-id="55f1e-204">In the Proxy server section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="55f1e-204">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="55f1e-205">![Proxy server](./media/zscaler-tutorial/ic769494.png "Proxy server")</span><span class="sxs-lookup"><span data-stu-id="55f1e-205">![Proxy server](./media/zscaler-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="55f1e-206">a.</span><span class="sxs-lookup"><span data-stu-id="55f1e-206">a.</span></span> <span data-ttu-id="55f1e-207">Select **Use a proxy server for your LAN**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-207">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="55f1e-208">b.</span><span class="sxs-lookup"><span data-stu-id="55f1e-208">b.</span></span> <span data-ttu-id="55f1e-209">In the Address textbox, type **gateway.zscaler.net**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-209">In the Address textbox, type **gateway.zscaler.net**.</span></span>

    <span data-ttu-id="55f1e-210">c.</span><span class="sxs-lookup"><span data-stu-id="55f1e-210">c.</span></span> <span data-ttu-id="55f1e-211">In the Port textbox, type **80**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-211">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="55f1e-212">d.</span><span class="sxs-lookup"><span data-stu-id="55f1e-212">d.</span></span> <span data-ttu-id="55f1e-213">Select **Bypass proxy server for local addresses**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-213">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="55f1e-214">e.</span><span class="sxs-lookup"><span data-stu-id="55f1e-214">e.</span></span> <span data-ttu-id="55f1e-215">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="55f1e-215">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

1. <span data-ttu-id="55f1e-216">Click **OK** to close the **Internet Options** dialog.</span><span class="sxs-lookup"><span data-stu-id="55f1e-216">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="55f1e-217">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="55f1e-217">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="55f1e-218">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="55f1e-218">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="55f1e-219">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="55f1e-219">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="55f1e-220">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="55f1e-220">Creating an Azure AD test user</span></span>
<span data-ttu-id="55f1e-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="55f1e-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="55f1e-223">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55f1e-223">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="55f1e-224">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="55f1e-224">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/zscaler-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="55f1e-226">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-226">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/zscaler-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="55f1e-228">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="55f1e-228">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/zscaler-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="55f1e-230">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="55f1e-230">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/zscaler-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="55f1e-232">a.</span><span class="sxs-lookup"><span data-stu-id="55f1e-232">a.</span></span> <span data-ttu-id="55f1e-233">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-233">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="55f1e-234">b.</span><span class="sxs-lookup"><span data-stu-id="55f1e-234">b.</span></span> <span data-ttu-id="55f1e-235">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="55f1e-235">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="55f1e-236">c.</span><span class="sxs-lookup"><span data-stu-id="55f1e-236">c.</span></span> <span data-ttu-id="55f1e-237">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-237">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="55f1e-238">d.</span><span class="sxs-lookup"><span data-stu-id="55f1e-238">d.</span></span> <span data-ttu-id="55f1e-239">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-239">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-test-user"></a><span data-ttu-id="55f1e-240">Creating a Zscaler test user</span><span class="sxs-lookup"><span data-stu-id="55f1e-240">Creating a Zscaler test user</span></span>

<span data-ttu-id="55f1e-241">To enable Azure AD users to log in to ZScaler, they must be provisioned to ZScaler.</span><span class="sxs-lookup"><span data-stu-id="55f1e-241">To enable Azure AD users to log in to ZScaler, they must be provisioned to ZScaler.</span></span>  
<span data-ttu-id="55f1e-242">In the case of ZScaler, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="55f1e-242">In the case of ZScaler, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="55f1e-243">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="55f1e-243">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="55f1e-244">Log in to your **Zscaler** tenant.</span><span class="sxs-lookup"><span data-stu-id="55f1e-244">Log in to your **Zscaler** tenant.</span></span>

1. <span data-ttu-id="55f1e-245">Click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-245">Click **Administration**.</span></span>   
   
    <span data-ttu-id="55f1e-246">![Administration](./media/zscaler-tutorial/ic781035.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="55f1e-246">![Administration](./media/zscaler-tutorial/ic781035.png "Administration")</span></span>

1. <span data-ttu-id="55f1e-247">Click **User Management**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-247">Click **User Management**.</span></span>   
        
     <span data-ttu-id="55f1e-248">![Add](./media/zscaler-tutorial/ic781036.png "Add")</span><span class="sxs-lookup"><span data-stu-id="55f1e-248">![Add](./media/zscaler-tutorial/ic781036.png "Add")</span></span>

1. <span data-ttu-id="55f1e-249">In the **Users** tab, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-249">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="55f1e-250">![Add](./media/zscaler-tutorial/ic781037.png "Add")</span><span class="sxs-lookup"><span data-stu-id="55f1e-250">![Add](./media/zscaler-tutorial/ic781037.png "Add")</span></span>

1. <span data-ttu-id="55f1e-251">In the Add User section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="55f1e-251">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="55f1e-252">![Add User](./media/zscaler-tutorial/ic781038.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="55f1e-252">![Add User](./media/zscaler-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="55f1e-253">a.</span><span class="sxs-lookup"><span data-stu-id="55f1e-253">a.</span></span> <span data-ttu-id="55f1e-254">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="55f1e-254">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="55f1e-255">b.</span><span class="sxs-lookup"><span data-stu-id="55f1e-255">b.</span></span> <span data-ttu-id="55f1e-256">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-256">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="55f1e-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="55f1e-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="55f1e-258">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="55f1e-258">Assigning the Azure AD test user</span></span>

<span data-ttu-id="55f1e-259">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler.</span><span class="sxs-lookup"><span data-stu-id="55f1e-259">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler.</span></span>

![Assign User][200] 

<span data-ttu-id="55f1e-261">**To assign Britta Simon to Zscaler, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="55f1e-261">**To assign Britta Simon to Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="55f1e-262">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-262">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="55f1e-264">In the applications list, select **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-264">In the applications list, select **Zscaler**.</span></span>

    ![Configure Single Sign-On](./media/zscaler-tutorial/tutorial_zscaler_app.png) 

1. <span data-ttu-id="55f1e-266">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="55f1e-266">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="55f1e-268">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="55f1e-268">Click **Add** button.</span></span> <span data-ttu-id="55f1e-269">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="55f1e-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="55f1e-271">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="55f1e-271">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="55f1e-272">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="55f1e-272">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="55f1e-273">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="55f1e-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="55f1e-274">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="55f1e-274">Testing single sign-on</span></span>

<span data-ttu-id="55f1e-275">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="55f1e-275">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="55f1e-276">When you click the Zscaler tile in the Access Panel, you should get automatically signed-on to your Zscaler application.</span><span class="sxs-lookup"><span data-stu-id="55f1e-276">When you click the Zscaler tile in the Access Panel, you should get automatically signed-on to your Zscaler application.</span></span>
<span data-ttu-id="55f1e-277">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="55f1e-277">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="55f1e-278">Additional resources</span><span class="sxs-lookup"><span data-stu-id="55f1e-278">Additional resources</span></span>

* [<span data-ttu-id="55f1e-279">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="55f1e-279">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="55f1e-280">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="55f1e-280">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/zscaler-tutorial/tutorial_general_01.png
[2]: ./media/zscaler-tutorial/tutorial_general_02.png
[3]: ./media/zscaler-tutorial/tutorial_general_03.png
[4]: ./media/zscaler-tutorial/tutorial_general_04.png

[100]: ./media/zscaler-tutorial/tutorial_general_100.png

[200]: ./media/zscaler-tutorial/tutorial_general_200.png
[201]: ./media/zscaler-tutorial/tutorial_general_201.png
[202]: ./media/zscaler-tutorial/tutorial_general_202.png
[203]: ./media/zscaler-tutorial/tutorial_general_203.png

