---
title: 'Tutorial: Azure Active Directory integration with Deputy | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Deputy.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: d4cf47dba0501694c5ed000c087f16d36b0dcdde
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856956"
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="61ccf-103">Tutorial: Azure Active Directory integration with Deputy</span><span class="sxs-lookup"><span data-stu-id="61ccf-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="61ccf-104">In this tutorial, you learn how to integrate Deputy with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61ccf-104">In this tutorial, you learn how to integrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61ccf-105">Integrating Deputy with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="61ccf-105">Integrating Deputy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="61ccf-106">You can control in Azure AD who has access to Deputy</span><span class="sxs-lookup"><span data-stu-id="61ccf-106">You can control in Azure AD who has access to Deputy</span></span>
- <span data-ttu-id="61ccf-107">You can enable your users to automatically get signed-on to Deputy (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="61ccf-107">You can enable your users to automatically get signed-on to Deputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="61ccf-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="61ccf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="61ccf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="61ccf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61ccf-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="61ccf-110">Prerequisites</span></span>

<span data-ttu-id="61ccf-111">To configure Azure AD integration with Deputy, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="61ccf-111">To configure Azure AD integration with Deputy, you need the following items:</span></span>

- <span data-ttu-id="61ccf-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="61ccf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61ccf-113">A Deputy single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="61ccf-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61ccf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="61ccf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61ccf-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="61ccf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61ccf-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="61ccf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61ccf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61ccf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61ccf-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="61ccf-118">Scenario description</span></span>
<span data-ttu-id="61ccf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="61ccf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61ccf-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="61ccf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61ccf-121">Adding Deputy from the gallery</span><span class="sxs-lookup"><span data-stu-id="61ccf-121">Adding Deputy from the gallery</span></span>
1. <span data-ttu-id="61ccf-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61ccf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-the-gallery"></a><span data-ttu-id="61ccf-123">Adding Deputy from the gallery</span><span class="sxs-lookup"><span data-stu-id="61ccf-123">Adding Deputy from the gallery</span></span>
<span data-ttu-id="61ccf-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="61ccf-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="61ccf-125">**To add Deputy from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61ccf-125">**To add Deputy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="61ccf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="61ccf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="61ccf-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="61ccf-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="61ccf-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="61ccf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="61ccf-133">In the search box, type **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-133">In the search box, type **Deputy**.</span></span>

    ![Creating an Azure AD test user](./media/deputy-tutorial/tutorial_deputy_search.png)

1. <span data-ttu-id="61ccf-135">In the results panel, select **Deputy**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="61ccf-135">In the results panel, select **Deputy**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="61ccf-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61ccf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="61ccf-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="61ccf-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="61ccf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Deputy is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61ccf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Deputy is to a user in Azure AD.</span></span> <span data-ttu-id="61ccf-140">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span><span class="sxs-lookup"><span data-stu-id="61ccf-140">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span></span>

<span data-ttu-id="61ccf-141">In Deputy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="61ccf-141">In Deputy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="61ccf-142">To configure and test Azure AD single sign-on with Deputy, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="61ccf-142">To configure and test Azure AD single sign-on with Deputy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="61ccf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="61ccf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="61ccf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61ccf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="61ccf-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="61ccf-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="61ccf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61ccf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="61ccf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="61ccf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="61ccf-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61ccf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="61ccf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Deputy application.</span><span class="sxs-lookup"><span data-stu-id="61ccf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="61ccf-150">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61ccf-150">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="61ccf-151">In the Azure portal, on the **Deputy** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-151">In the Azure portal, on the **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="61ccf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61ccf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/deputy-tutorial/tutorial_deputy_samlbase.png)

1. <span data-ttu-id="61ccf-155">On the **Deputy Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="61ccf-155">On the **Deputy Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="61ccf-157">a.</span><span class="sxs-lookup"><span data-stu-id="61ccf-157">a.</span></span> <span data-ttu-id="61ccf-158">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="61ccf-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="61ccf-159">b.</span><span class="sxs-lookup"><span data-stu-id="61ccf-159">b.</span></span> <span data-ttu-id="61ccf-160">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="61ccf-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

1. <span data-ttu-id="61ccf-161">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="61ccf-162">If you wish to configure the application in **SP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="61ccf-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="61ccf-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="61ccf-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="61ccf-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span><span class="sxs-lookup"><span data-stu-id="61ccf-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="61ccf-166">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="61ccf-166">These values are not real.</span></span> <span data-ttu-id="61ccf-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="61ccf-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="61ccf-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) to get these values.</span><span class="sxs-lookup"><span data-stu-id="61ccf-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) to get these values.</span></span> 

1. <span data-ttu-id="61ccf-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="61ccf-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/deputy-tutorial/tutorial_deputy_certificate.png) 

1. <span data-ttu-id="61ccf-171">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="61ccf-171">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/deputy-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="61ccf-173">On the **Deputy Configuration** section, click **Configure Deputy** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="61ccf-173">On the **Deputy Configuration** section, click **Configure Deputy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="61ccf-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="61ccf-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/deputy-tutorial/tutorial_deputy_configure.png) 

1. <span data-ttu-id="61ccf-176">Navigate to the following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="61ccf-176">Navigate to the following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="61ccf-177">Go to **Security Settings** and click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-177">Go to **Security Settings** and click **Edit**.</span></span>
   
    ![Configure Single Sign-On](./media/deputy-tutorial/tutorial_deputy_004.png)

1. <span data-ttu-id="61ccf-179">On this **Security Settings** page, perform below steps.</span><span class="sxs-lookup"><span data-stu-id="61ccf-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Configure Single Sign-On](./media/deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="61ccf-181">a.</span><span class="sxs-lookup"><span data-stu-id="61ccf-181">a.</span></span> <span data-ttu-id="61ccf-182">Enable **Social Login**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="61ccf-183">b.</span><span class="sxs-lookup"><span data-stu-id="61ccf-183">b.</span></span> <span data-ttu-id="61ccf-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="61ccf-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="61ccf-185">c.</span><span class="sxs-lookup"><span data-stu-id="61ccf-185">c.</span></span> <span data-ttu-id="61ccf-186">In the SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="61ccf-186">In the SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="61ccf-187">d.</span><span class="sxs-lookup"><span data-stu-id="61ccf-187">d.</span></span> <span data-ttu-id="61ccf-188">In the SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span><span class="sxs-lookup"><span data-stu-id="61ccf-188">In the SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="61ccf-189">e.</span><span class="sxs-lookup"><span data-stu-id="61ccf-189">e.</span></span> <span data-ttu-id="61ccf-190">In the SAML SSO URL textbox, replace `<saml sso url>` with the **SAML Single Sign-On Service URL** you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="61ccf-190">In the SAML SSO URL textbox, replace `<saml sso url>` with the **SAML Single Sign-On Service URL** you have copied from the Azure portal.</span></span>
   
    <span data-ttu-id="61ccf-191">f.</span><span class="sxs-lookup"><span data-stu-id="61ccf-191">f.</span></span> <span data-ttu-id="61ccf-192">Click **Save Settings**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="61ccf-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="61ccf-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="61ccf-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="61ccf-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="61ccf-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="61ccf-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="61ccf-196">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="61ccf-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="61ccf-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61ccf-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="61ccf-199">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61ccf-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="61ccf-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="61ccf-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/deputy-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="61ccf-202">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/deputy-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="61ccf-204">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="61ccf-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/deputy-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="61ccf-206">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61ccf-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="61ccf-208">a.</span><span class="sxs-lookup"><span data-stu-id="61ccf-208">a.</span></span> <span data-ttu-id="61ccf-209">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61ccf-210">b.</span><span class="sxs-lookup"><span data-stu-id="61ccf-210">b.</span></span> <span data-ttu-id="61ccf-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="61ccf-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="61ccf-212">c.</span><span class="sxs-lookup"><span data-stu-id="61ccf-212">c.</span></span> <span data-ttu-id="61ccf-213">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="61ccf-214">d.</span><span class="sxs-lookup"><span data-stu-id="61ccf-214">d.</span></span> <span data-ttu-id="61ccf-215">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="61ccf-216">Creating a Deputy test user</span><span class="sxs-lookup"><span data-stu-id="61ccf-216">Creating a Deputy test user</span></span>

<span data-ttu-id="61ccf-217">To enable Azure AD users to log in to Deputy, they must be provisioned into Deputy.</span><span class="sxs-lookup"><span data-stu-id="61ccf-217">To enable Azure AD users to log in to Deputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="61ccf-218">In case of Deputy, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="61ccf-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="61ccf-219">To provision a user account, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61ccf-219">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="61ccf-220">Log in to your Deputy company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="61ccf-220">Log in to your Deputy company site as an administrator.</span></span>

1. <span data-ttu-id="61ccf-221">On the top navigation pane, click **People**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-221">On the top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="61ccf-222">![People](./media/deputy-tutorial/tutorial_deputy_001.png "People")</span><span class="sxs-lookup"><span data-stu-id="61ccf-222">![People](./media/deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

1. <span data-ttu-id="61ccf-223">Click the **Add People** button and click **Add a single person**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-223">Click the **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="61ccf-224">![Add People](./media/deputy-tutorial/tutorial_deputy_002.png "Add People")</span><span class="sxs-lookup"><span data-stu-id="61ccf-224">![Add People](./media/deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

1. <span data-ttu-id="61ccf-225">Perform the following steps and click **Save & Invite**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-225">Perform the following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="61ccf-226">![New User](./media/deputy-tutorial/tutorial_deputy_003.png "New User")</span><span class="sxs-lookup"><span data-stu-id="61ccf-226">![New User](./media/deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="61ccf-227">a.</span><span class="sxs-lookup"><span data-stu-id="61ccf-227">a.</span></span> <span data-ttu-id="61ccf-228">In the **Name** textbox, type name of the user like **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-228">In the **Name** textbox, type name of the user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="61ccf-229">b.</span><span class="sxs-lookup"><span data-stu-id="61ccf-229">b.</span></span> <span data-ttu-id="61ccf-230">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="61ccf-230">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span></span>
   
   <span data-ttu-id="61ccf-231">c.</span><span class="sxs-lookup"><span data-stu-id="61ccf-231">c.</span></span> <span data-ttu-id="61ccf-232">In the **Work at** textbox, type the business name.</span><span class="sxs-lookup"><span data-stu-id="61ccf-232">In the **Work at** textbox, type the business name.</span></span>
   
   <span data-ttu-id="61ccf-233">d.</span><span class="sxs-lookup"><span data-stu-id="61ccf-233">d.</span></span> <span data-ttu-id="61ccf-234">Click **Save & Invite** button.</span><span class="sxs-lookup"><span data-stu-id="61ccf-234">Click **Save & Invite** button.</span></span>

1. <span data-ttu-id="61ccf-235">The AAD account holder receives an email and follows a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="61ccf-235">The AAD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="61ccf-236">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="61ccf-236">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="61ccf-237">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="61ccf-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="61ccf-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Deputy.</span><span class="sxs-lookup"><span data-stu-id="61ccf-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Deputy.</span></span>

![Assign User][200] 

<span data-ttu-id="61ccf-240">**To assign Britta Simon to Deputy, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61ccf-240">**To assign Britta Simon to Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="61ccf-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="61ccf-243">In the applications list, select **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-243">In the applications list, select **Deputy**.</span></span>

    ![Configure Single Sign-On](./media/deputy-tutorial/tutorial_deputy_app.png) 

1. <span data-ttu-id="61ccf-245">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="61ccf-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="61ccf-247">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="61ccf-247">Click **Add** button.</span></span> <span data-ttu-id="61ccf-248">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="61ccf-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="61ccf-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="61ccf-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="61ccf-251">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="61ccf-251">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="61ccf-252">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="61ccf-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="61ccf-253">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="61ccf-253">Testing single sign-on</span></span>

<span data-ttu-id="61ccf-254">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="61ccf-254">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="61ccf-255">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span><span class="sxs-lookup"><span data-stu-id="61ccf-255">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="61ccf-256">Additional resources</span><span class="sxs-lookup"><span data-stu-id="61ccf-256">Additional resources</span></span>

* [<span data-ttu-id="61ccf-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61ccf-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="61ccf-258">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61ccf-258">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/deputy-tutorial/tutorial_general_01.png
[2]: ./media/deputy-tutorial/tutorial_general_02.png
[3]: ./media/deputy-tutorial/tutorial_general_03.png
[4]: ./media/deputy-tutorial/tutorial_general_04.png

[100]: ./media/deputy-tutorial/tutorial_general_100.png

[200]: ./media/deputy-tutorial/tutorial_general_200.png
[201]: ./media/deputy-tutorial/tutorial_general_201.png
[202]: ./media/deputy-tutorial/tutorial_general_202.png
[203]: ./media/deputy-tutorial/tutorial_general_203.png

