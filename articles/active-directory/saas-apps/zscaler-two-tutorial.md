---
title: 'Tutorial: Azure Active Directory integration with Zscaler Two | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Zscaler Two.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 1fd8a940-7320-47e0-a176-2dd4eeca6db2
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4f44f6eef4c40f60de8af0a7ca517b0f28cd34f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867816"
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-two"></a><span data-ttu-id="61a7d-103">Tutorial: Azure Active Directory integration with Zscaler Two</span><span class="sxs-lookup"><span data-stu-id="61a7d-103">Tutorial: Azure Active Directory integration with Zscaler Two</span></span>

<span data-ttu-id="61a7d-104">In this tutorial, you learn how to integrate Zscaler Two with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61a7d-104">In this tutorial, you learn how to integrate Zscaler Two with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61a7d-105">Integrating Zscaler Two with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="61a7d-105">Integrating Zscaler Two with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="61a7d-106">You can control in Azure AD who has access to Zscaler Two</span><span class="sxs-lookup"><span data-stu-id="61a7d-106">You can control in Azure AD who has access to Zscaler Two</span></span>
- <span data-ttu-id="61a7d-107">You can enable your users to automatically get signed-on to Zscaler Two (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="61a7d-107">You can enable your users to automatically get signed-on to Zscaler Two (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="61a7d-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="61a7d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="61a7d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="61a7d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61a7d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="61a7d-110">Prerequisites</span></span>

<span data-ttu-id="61a7d-111">To configure Azure AD integration with Zscaler Two, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="61a7d-111">To configure Azure AD integration with Zscaler Two, you need the following items:</span></span>

- <span data-ttu-id="61a7d-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="61a7d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61a7d-113">A Zscaler Two single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="61a7d-113">A Zscaler Two single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61a7d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="61a7d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61a7d-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="61a7d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61a7d-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="61a7d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61a7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61a7d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61a7d-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="61a7d-118">Scenario description</span></span>
<span data-ttu-id="61a7d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="61a7d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61a7d-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="61a7d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61a7d-121">Adding Zscaler Two from the gallery</span><span class="sxs-lookup"><span data-stu-id="61a7d-121">Adding Zscaler Two from the gallery</span></span>
1. <span data-ttu-id="61a7d-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61a7d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-two-from-the-gallery"></a><span data-ttu-id="61a7d-123">Adding Zscaler Two from the gallery</span><span class="sxs-lookup"><span data-stu-id="61a7d-123">Adding Zscaler Two from the gallery</span></span>
<span data-ttu-id="61a7d-124">To configure the integration of Zscaler Two into Azure AD, you need to add Zscaler Two from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="61a7d-124">To configure the integration of Zscaler Two into Azure AD, you need to add Zscaler Two from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="61a7d-125">**To add Zscaler Two from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61a7d-125">**To add Zscaler Two from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="61a7d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="61a7d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="61a7d-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="61a7d-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="61a7d-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="61a7d-133">In the search box, type **Zscaler Two**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-133">In the search box, type **Zscaler Two**.</span></span>

    ![Creating an Azure AD test user](./media/zscaler-two-tutorial/tutorial_zscalertwo_search.png)

1. <span data-ttu-id="61a7d-135">In the results panel, select **Zscaler Two**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="61a7d-135">In the results panel, select **Zscaler Two**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/zscaler-two-tutorial/tutorial_zscalertwo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="61a7d-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61a7d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="61a7d-138">In this section, you configure and test Azure AD single sign-on with Zscaler Two based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="61a7d-138">In this section, you configure and test Azure AD single sign-on with Zscaler Two based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="61a7d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Two is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61a7d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Two is to a user in Azure AD.</span></span> <span data-ttu-id="61a7d-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Two needs to be established.</span><span class="sxs-lookup"><span data-stu-id="61a7d-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Two needs to be established.</span></span>

<span data-ttu-id="61a7d-141">In Zscaler Two, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="61a7d-141">In Zscaler Two, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="61a7d-142">To configure and test Azure AD single sign-on with Zscaler Two, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="61a7d-142">To configure and test Azure AD single sign-on with Zscaler Two, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="61a7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="61a7d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="61a7d-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="61a7d-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
1. <span data-ttu-id="61a7d-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61a7d-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="61a7d-146">**[Creating a Zscaler Two test user](#creating-a-zscaler-two-test-user)** - to have a counterpart of Britta Simon in Zscaler Two that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="61a7d-146">**[Creating a Zscaler Two test user](#creating-a-zscaler-two-test-user)** - to have a counterpart of Britta Simon in Zscaler Two that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="61a7d-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61a7d-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="61a7d-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="61a7d-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="61a7d-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61a7d-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="61a7d-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler Two application.</span><span class="sxs-lookup"><span data-stu-id="61a7d-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler Two application.</span></span>

<span data-ttu-id="61a7d-151">**To configure Azure AD single sign-on with Zscaler Two, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61a7d-151">**To configure Azure AD single sign-on with Zscaler Two, perform the following steps:**</span></span>

1. <span data-ttu-id="61a7d-152">In the Azure portal, on the **Zscaler Two** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-152">In the Azure portal, on the **Zscaler Two** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="61a7d-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61a7d-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/zscaler-two-tutorial/tutorial_zscalertwo_samlbase.png)

1. <span data-ttu-id="61a7d-156">On the **Zscaler Two Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61a7d-156">On the **Zscaler Two Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/zscaler-two-tutorial/tutorial_zscalertwo_url.png)

   <span data-ttu-id="61a7d-158">In the Sign-on URL textbox, type the URL used by your users to sign-on to your ZScaler Two application.</span><span class="sxs-lookup"><span data-stu-id="61a7d-158">In the Sign-on URL textbox, type the URL used by your users to sign-on to your ZScaler Two application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="61a7d-159">You have to update this value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="61a7d-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="61a7d-160">Contact [Zscaler Two Client support team](https://www.zscaler.com/company/contact) to get these values.</span><span class="sxs-lookup"><span data-stu-id="61a7d-160">Contact [Zscaler Two Client support team](https://www.zscaler.com/company/contact) to get these values.</span></span>

1. <span data-ttu-id="61a7d-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="61a7d-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/zscaler-two-tutorial/tutorial_zscalertwo_certificate.png) 

1. <span data-ttu-id="61a7d-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="61a7d-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/zscaler-two-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="61a7d-165">On the **Zscaler Two Configuration** section, click **Configure Zscaler Two** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="61a7d-165">On the **Zscaler Two Configuration** section, click **Configure Zscaler Two** to open **Configure sign-on** window.</span></span> <span data-ttu-id="61a7d-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="61a7d-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/zscaler-two-tutorial/tutorial_zscalertwo_configure.png) 

1. <span data-ttu-id="61a7d-168">In a different web browser window, log in to your ZScaler Two company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="61a7d-168">In a different web browser window, log in to your ZScaler Two company site as an administrator.</span></span>

1. <span data-ttu-id="61a7d-169">In the menu on the top, click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="61a7d-170">![Administration](./media/zscaler-two-tutorial/ic800206.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="61a7d-170">![Administration](./media/zscaler-two-tutorial/ic800206.png "Administration")</span></span>

1. <span data-ttu-id="61a7d-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="61a7d-172">![Manage Users & Authentication](./media/zscaler-two-tutorial/ic800207.png "Manage Users & Authentication")</span><span class="sxs-lookup"><span data-stu-id="61a7d-172">![Manage Users & Authentication](./media/zscaler-two-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

1. <span data-ttu-id="61a7d-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61a7d-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="61a7d-174">![Authentication](./media/zscaler-two-tutorial/ic800208.png "Authentication")</span><span class="sxs-lookup"><span data-stu-id="61a7d-174">![Authentication](./media/zscaler-two-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="61a7d-175">a.</span><span class="sxs-lookup"><span data-stu-id="61a7d-175">a.</span></span> <span data-ttu-id="61a7d-176">Select **Authenticate using SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="61a7d-177">b.</span><span class="sxs-lookup"><span data-stu-id="61a7d-177">b.</span></span> <span data-ttu-id="61a7d-178">Click **Configure SAML Single Sign-On Parameters**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

1. <span data-ttu-id="61a7d-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span><span class="sxs-lookup"><span data-stu-id="61a7d-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="61a7d-180">![Single Sign-On](./media/zscaler-two-tutorial/ic800209.png "Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="61a7d-180">![Single Sign-On](./media/zscaler-two-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="61a7d-181">a.</span><span class="sxs-lookup"><span data-stu-id="61a7d-181">a.</span></span> <span data-ttu-id="61a7d-182">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span><span class="sxs-lookup"><span data-stu-id="61a7d-182">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="61a7d-183">b.</span><span class="sxs-lookup"><span data-stu-id="61a7d-183">b.</span></span> <span data-ttu-id="61a7d-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="61a7d-185">c.</span><span class="sxs-lookup"><span data-stu-id="61a7d-185">c.</span></span> <span data-ttu-id="61a7d-186">To upload your downloaded certificate, click **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="61a7d-187">d.</span><span class="sxs-lookup"><span data-stu-id="61a7d-187">d.</span></span> <span data-ttu-id="61a7d-188">Select **Enable SAML Auto-Provisioning**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-188">Select **Enable SAML Auto-Provisioning**.</span></span>

1. <span data-ttu-id="61a7d-189">On the **Configure User Authentication** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61a7d-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="61a7d-190">![Administration](./media/zscaler-two-tutorial/ic800210.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="61a7d-190">![Administration](./media/zscaler-two-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="61a7d-191">a.</span><span class="sxs-lookup"><span data-stu-id="61a7d-191">a.</span></span> <span data-ttu-id="61a7d-192">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-192">Click **Save**.</span></span>

    <span data-ttu-id="61a7d-193">b.</span><span class="sxs-lookup"><span data-stu-id="61a7d-193">b.</span></span> <span data-ttu-id="61a7d-194">Click **Activate Now**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="61a7d-195">Configuring proxy settings</span><span class="sxs-lookup"><span data-stu-id="61a7d-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="61a7d-196">To configure the proxy settings in Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="61a7d-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="61a7d-197">Start **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-197">Start **Internet Explorer**.</span></span>

1. <span data-ttu-id="61a7d-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7d-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="61a7d-199">![Internet Options](./media/zscaler-two-tutorial/ic769492.png "Internet Options")</span><span class="sxs-lookup"><span data-stu-id="61a7d-199">![Internet Options](./media/zscaler-two-tutorial/ic769492.png "Internet Options")</span></span>

1. <span data-ttu-id="61a7d-200">Click the **Connections** tab.</span><span class="sxs-lookup"><span data-stu-id="61a7d-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="61a7d-201">![Connections](./media/zscaler-two-tutorial/ic769493.png "Connections")</span><span class="sxs-lookup"><span data-stu-id="61a7d-201">![Connections](./media/zscaler-two-tutorial/ic769493.png "Connections")</span></span>

1. <span data-ttu-id="61a7d-202">Click **LAN settings** to open the **LAN Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7d-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

1. <span data-ttu-id="61a7d-203">In the Proxy server section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61a7d-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="61a7d-204">![Proxy server](./media/zscaler-two-tutorial/ic769494.png "Proxy server")</span><span class="sxs-lookup"><span data-stu-id="61a7d-204">![Proxy server](./media/zscaler-two-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="61a7d-205">a.</span><span class="sxs-lookup"><span data-stu-id="61a7d-205">a.</span></span> <span data-ttu-id="61a7d-206">Select **Use a proxy server for your LAN**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="61a7d-207">b.</span><span class="sxs-lookup"><span data-stu-id="61a7d-207">b.</span></span> <span data-ttu-id="61a7d-208">In the Address textbox, type **gateway.zscalertwo.net**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-208">In the Address textbox, type **gateway.zscalertwo.net**.</span></span>

    <span data-ttu-id="61a7d-209">c.</span><span class="sxs-lookup"><span data-stu-id="61a7d-209">c.</span></span> <span data-ttu-id="61a7d-210">In the Port textbox, type **80**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="61a7d-211">d.</span><span class="sxs-lookup"><span data-stu-id="61a7d-211">d.</span></span> <span data-ttu-id="61a7d-212">Select **Bypass proxy server for local addresses**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="61a7d-213">e.</span><span class="sxs-lookup"><span data-stu-id="61a7d-213">e.</span></span> <span data-ttu-id="61a7d-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7d-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

1. <span data-ttu-id="61a7d-215">Click **OK** to close the **Internet Options** dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7d-215">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="61a7d-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="61a7d-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="61a7d-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="61a7d-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="61a7d-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="61a7d-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="61a7d-219">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="61a7d-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="61a7d-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61a7d-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="61a7d-222">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61a7d-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="61a7d-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="61a7d-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/zscaler-two-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="61a7d-225">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/zscaler-two-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="61a7d-227">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7d-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/zscaler-two-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="61a7d-229">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61a7d-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/zscaler-two-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="61a7d-231">a.</span><span class="sxs-lookup"><span data-stu-id="61a7d-231">a.</span></span> <span data-ttu-id="61a7d-232">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61a7d-233">b.</span><span class="sxs-lookup"><span data-stu-id="61a7d-233">b.</span></span> <span data-ttu-id="61a7d-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="61a7d-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="61a7d-235">c.</span><span class="sxs-lookup"><span data-stu-id="61a7d-235">c.</span></span> <span data-ttu-id="61a7d-236">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="61a7d-237">d.</span><span class="sxs-lookup"><span data-stu-id="61a7d-237">d.</span></span> <span data-ttu-id="61a7d-238">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-two-test-user"></a><span data-ttu-id="61a7d-239">Creating a Zscaler Two test user</span><span class="sxs-lookup"><span data-stu-id="61a7d-239">Creating a Zscaler Two test user</span></span>

<span data-ttu-id="61a7d-240">To enable Azure AD users to log in to ZScaler Two, they must be provisioned to ZScaler Two.</span><span class="sxs-lookup"><span data-stu-id="61a7d-240">To enable Azure AD users to log in to ZScaler Two, they must be provisioned to ZScaler Two.</span></span> <span data-ttu-id="61a7d-241">In the case of ZScaler Two, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="61a7d-241">In the case of ZScaler Two, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="61a7d-242">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61a7d-242">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="61a7d-243">Log in to your **Zscaler Two** tenant.</span><span class="sxs-lookup"><span data-stu-id="61a7d-243">Log in to your **Zscaler Two** tenant.</span></span>

1. <span data-ttu-id="61a7d-244">Click **Administration**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="61a7d-245">![Administration](./media/zscaler-two-tutorial/ic781035.png "Administration")</span><span class="sxs-lookup"><span data-stu-id="61a7d-245">![Administration](./media/zscaler-two-tutorial/ic781035.png "Administration")</span></span>

1. <span data-ttu-id="61a7d-246">Click **User Management**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="61a7d-247">![Add](./media/zscaler-two-tutorial/ic781036.png "Add")</span><span class="sxs-lookup"><span data-stu-id="61a7d-247">![Add](./media/zscaler-two-tutorial/ic781036.png "Add")</span></span>

1. <span data-ttu-id="61a7d-248">In the **Users** tab, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-248">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="61a7d-249">![Add](./media/zscaler-two-tutorial/ic781037.png "Add")</span><span class="sxs-lookup"><span data-stu-id="61a7d-249">![Add](./media/zscaler-two-tutorial/ic781037.png "Add")</span></span>

1. <span data-ttu-id="61a7d-250">In the Add User section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61a7d-250">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="61a7d-251">![Add User](./media/zscaler-two-tutorial/ic781038.png "Add User")</span><span class="sxs-lookup"><span data-stu-id="61a7d-251">![Add User](./media/zscaler-two-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="61a7d-252">a.</span><span class="sxs-lookup"><span data-stu-id="61a7d-252">a.</span></span> <span data-ttu-id="61a7d-253">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="61a7d-253">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="61a7d-254">b.</span><span class="sxs-lookup"><span data-stu-id="61a7d-254">b.</span></span> <span data-ttu-id="61a7d-255">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="61a7d-256">You can use any other ZScaler Two user account creation tools or APIs provided by ZScaler Two to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="61a7d-256">You can use any other ZScaler Two user account creation tools or APIs provided by ZScaler Two to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="61a7d-257">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="61a7d-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="61a7d-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="61a7d-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler Two.</span></span>

![Assign User][200] 

<span data-ttu-id="61a7d-260">**To assign Britta Simon to Zscaler Two, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61a7d-260">**To assign Britta Simon to Zscaler Two, perform the following steps:**</span></span>

1. <span data-ttu-id="61a7d-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="61a7d-263">In the applications list, select **Zscaler Two**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-263">In the applications list, select **Zscaler Two**.</span></span>

    ![Configure Single Sign-On](./media/zscaler-two-tutorial/tutorial_zscalertwo_app.png) 

1. <span data-ttu-id="61a7d-265">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="61a7d-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="61a7d-267">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="61a7d-267">Click **Add** button.</span></span> <span data-ttu-id="61a7d-268">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7d-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="61a7d-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="61a7d-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="61a7d-271">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7d-271">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="61a7d-272">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7d-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="61a7d-273">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="61a7d-273">Testing single sign-on</span></span>

<span data-ttu-id="61a7d-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="61a7d-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="61a7d-275">When you click the Zscaler Two tile in the Access Panel, you should get automatically signed-on to your Zscaler Two application.</span><span class="sxs-lookup"><span data-stu-id="61a7d-275">When you click the Zscaler Two tile in the Access Panel, you should get automatically signed-on to your Zscaler Two application.</span></span>
<span data-ttu-id="61a7d-276">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="61a7d-276">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="61a7d-277">Additional resources</span><span class="sxs-lookup"><span data-stu-id="61a7d-277">Additional resources</span></span>

* [<span data-ttu-id="61a7d-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61a7d-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="61a7d-279">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61a7d-279">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/zscaler-two-tutorial/tutorial_general_01.png
[2]: ./media/zscaler-two-tutorial/tutorial_general_02.png
[3]: ./media/zscaler-two-tutorial/tutorial_general_03.png
[4]: ./media/zscaler-two-tutorial/tutorial_general_04.png

[100]: ./media/zscaler-two-tutorial/tutorial_general_100.png

[200]: ./media/zscaler-two-tutorial/tutorial_general_200.png
[201]: ./media/zscaler-two-tutorial/tutorial_general_201.png
[202]: ./media/zscaler-two-tutorial/tutorial_general_202.png
[203]: ./media/zscaler-two-tutorial/tutorial_general_203.png

