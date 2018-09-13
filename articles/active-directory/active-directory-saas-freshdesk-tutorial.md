---
title: 'Tutorial: Azure Active Directory integration with FreshDesk | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and FreshDesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: bfcfbd92beeb952186d3cb561ac29805c3f87ea5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540935"
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="38d1e-103">Tutorial: Azure Active Directory integration with FreshDesk</span><span class="sxs-lookup"><span data-stu-id="38d1e-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="38d1e-104">In this tutorial, you learn how to integrate FreshDesk with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38d1e-104">In this tutorial, you learn how to integrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38d1e-105">Integrating FreshDesk with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="38d1e-105">Integrating FreshDesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="38d1e-106">You can control in Azure AD who has access to FreshDesk</span><span class="sxs-lookup"><span data-stu-id="38d1e-106">You can control in Azure AD who has access to FreshDesk</span></span>
- <span data-ttu-id="38d1e-107">You can enable your users to automatically get signed-on to FreshDesk (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="38d1e-107">You can enable your users to automatically get signed-on to FreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="38d1e-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="38d1e-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="38d1e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38d1e-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38d1e-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="38d1e-110">Prerequisites</span></span>

<span data-ttu-id="38d1e-111">To configure Azure AD integration with FreshDesk, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="38d1e-111">To configure Azure AD integration with FreshDesk, you need the following items:</span></span>

- <span data-ttu-id="38d1e-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="38d1e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38d1e-113">A FreshDesk single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="38d1e-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38d1e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="38d1e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38d1e-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="38d1e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38d1e-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="38d1e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="38d1e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38d1e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38d1e-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="38d1e-118">Scenario description</span></span>
<span data-ttu-id="38d1e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="38d1e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38d1e-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="38d1e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38d1e-121">Adding FreshDesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="38d1e-121">Adding FreshDesk from the gallery</span></span>
2. <span data-ttu-id="38d1e-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="38d1e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-the-gallery"></a><span data-ttu-id="38d1e-123">Adding FreshDesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="38d1e-123">Adding FreshDesk from the gallery</span></span>
<span data-ttu-id="38d1e-124">To configure the integration of FreshDesk into Azure AD, you need to add FreshDesk from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="38d1e-124">To configure the integration of FreshDesk into Azure AD, you need to add FreshDesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="38d1e-125">**To add FreshDesk from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="38d1e-125">**To add FreshDesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="38d1e-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="38d1e-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="38d1e-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="38d1e-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="38d1e-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="38d1e-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="38d1e-133">In the search box, type **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-133">In the search box, type **FreshDesk**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_search.png)

5. <span data-ttu-id="38d1e-135">In the results panel, select **FreshDesk**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="38d1e-135">In the results panel, select **FreshDesk**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="38d1e-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="38d1e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="38d1e-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="38d1e-138">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="38d1e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshDesk is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38d1e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshDesk is to a user in Azure AD.</span></span> <span data-ttu-id="38d1e-140">In other words, a link relationship between an Azure AD user and the related user in FreshDesk needs to be established.</span><span class="sxs-lookup"><span data-stu-id="38d1e-140">In other words, a link relationship between an Azure AD user and the related user in FreshDesk needs to be established.</span></span>

<span data-ttu-id="38d1e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="38d1e-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshDesk.</span></span>

<span data-ttu-id="38d1e-142">To configure and test Azure AD single sign-on with FreshDesk, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="38d1e-142">To configure and test Azure AD single sign-on with FreshDesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="38d1e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="38d1e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="38d1e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38d1e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38d1e-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - to have a counterpart of Britta Simon in FreshDesk that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="38d1e-145">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - to have a counterpart of Britta Simon in FreshDesk that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="38d1e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="38d1e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38d1e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="38d1e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="38d1e-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="38d1e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="38d1e-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FreshDesk application.</span><span class="sxs-lookup"><span data-stu-id="38d1e-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="38d1e-150">**To configure Azure AD single sign-on with FreshDesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="38d1e-150">**To configure Azure AD single sign-on with FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="38d1e-151">In the Azure Management portal, on the **FreshDesk** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-151">In the Azure Management portal, on the **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="38d1e-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="38d1e-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="38d1e-155">On the **FreshDesk Domain and URLs** section, please enter the **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span><span class="sxs-lookup"><span data-stu-id="38d1e-155">On the **FreshDesk Domain and URLs** section, please enter the **Sign-on URL** as: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_url.png)

    > [!NOTE] 
    > <span data-ttu-id="38d1e-157">Please note that this is not the real value.</span><span class="sxs-lookup"><span data-stu-id="38d1e-157">Please note that this is not the real value.</span></span> <span data-ttu-id="38d1e-158">You have to update the value with the actual Sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="38d1e-158">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="38d1e-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span><span class="sxs-lookup"><span data-stu-id="38d1e-159">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="38d1e-160">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span><span class="sxs-lookup"><span data-stu-id="38d1e-160">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_certificate.png) 

5. <span data-ttu-id="38d1e-162">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="38d1e-162">Click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="38d1e-164">On the **FreshDesk Configuration** section, click **Configure FreshDesk** to open Configure sign-on window.</span><span class="sxs-lookup"><span data-stu-id="38d1e-164">On the **FreshDesk Configuration** section, click **Configure FreshDesk** to open Configure sign-on window.</span></span> <span data-ttu-id="38d1e-165">Copy the SAML Single Sign-On Service URL and Sign-Out URL from the **Quick Reference** section.</span><span class="sxs-lookup"><span data-stu-id="38d1e-165">Copy the SAML Single Sign-On Service URL and Sign-Out URL from the **Quick Reference** section.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_configure.png)

7. <span data-ttu-id="38d1e-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="38d1e-167">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

8. <span data-ttu-id="38d1e-168">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-168">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="38d1e-169">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="38d1e-169">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776768.png "Admin")</span></span>

9. <span data-ttu-id="38d1e-170">In the **General Settings** tab, click **Security**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-170">In the **General Settings** tab, click **Security**.</span></span>
   
    <span data-ttu-id="38d1e-171">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span><span class="sxs-lookup"><span data-stu-id="38d1e-171">![Security](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776769.png "Security")</span></span>

10. <span data-ttu-id="38d1e-172">In the **Security** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="38d1e-172">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="38d1e-173">![Single Sign On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span><span class="sxs-lookup"><span data-stu-id="38d1e-173">![Single Sign On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
   
    <span data-ttu-id="38d1e-174">a.</span><span class="sxs-lookup"><span data-stu-id="38d1e-174">a.</span></span> <span data-ttu-id="38d1e-175">For **Single Sign On (SSO)**, select **On**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-175">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="38d1e-176">b.</span><span class="sxs-lookup"><span data-stu-id="38d1e-176">b.</span></span> <span data-ttu-id="38d1e-177">Select **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-177">Select **SAML SSO**.</span></span>

    <span data-ttu-id="38d1e-178">c.</span><span class="sxs-lookup"><span data-stu-id="38d1e-178">c.</span></span> <span data-ttu-id="38d1e-179">Type the **SAML Single Sign-On Service URL** you copied from Azure portal into the **SAML Login URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="38d1e-179">Type the **SAML Single Sign-On Service URL** you copied from Azure portal into the **SAML Login URL** textbox.</span></span>

    <span data-ttu-id="38d1e-180">d.</span><span class="sxs-lookup"><span data-stu-id="38d1e-180">d.</span></span> <span data-ttu-id="38d1e-181">Type the **Sign-Out URL**  you copied from Azure portal into the **Logout URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="38d1e-181">Type the **Sign-Out URL**  you copied from Azure portal into the **Logout URL** textbox.</span></span>

    <span data-ttu-id="38d1e-182">e.</span><span class="sxs-lookup"><span data-stu-id="38d1e-182">e.</span></span> <span data-ttu-id="38d1e-183">Copy the **Thumbprint** value from the downloaded certificate from Azure portal and paste it into the **Security Certificate Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="38d1e-183">Copy the **Thumbprint** value from the downloaded certificate from Azure portal and paste it into the **Security Certificate Fingerprint** textbox.</span></span>  
 
    >[!TIP]
    ><span data-ttu-id="38d1e-184">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="38d1e-184">For more details, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span> 
    
    <span data-ttu-id="38d1e-185">f.</span><span class="sxs-lookup"><span data-stu-id="38d1e-185">f.</span></span> <span data-ttu-id="38d1e-186">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-186">Click **Save**.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="38d1e-187">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="38d1e-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="38d1e-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38d1e-188">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="38d1e-190">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="38d1e-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="38d1e-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="38d1e-191">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="38d1e-193">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="38d1e-193">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="38d1e-195">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="38d1e-195">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="38d1e-197">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="38d1e-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="38d1e-199">a.</span><span class="sxs-lookup"><span data-stu-id="38d1e-199">a.</span></span> <span data-ttu-id="38d1e-200">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38d1e-201">b.</span><span class="sxs-lookup"><span data-stu-id="38d1e-201">b.</span></span> <span data-ttu-id="38d1e-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="38d1e-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="38d1e-203">c.</span><span class="sxs-lookup"><span data-stu-id="38d1e-203">c.</span></span> <span data-ttu-id="38d1e-204">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="38d1e-205">d.</span><span class="sxs-lookup"><span data-stu-id="38d1e-205">d.</span></span> <span data-ttu-id="38d1e-206">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-206">Click **Create**.</span></span>
 
### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="38d1e-207">Creating a FreshDesk test user</span><span class="sxs-lookup"><span data-stu-id="38d1e-207">Creating a FreshDesk test user</span></span>

<span data-ttu-id="38d1e-208">In order to enable Azure AD users to log into FreshDesk, they must be provisioned into FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="38d1e-208">In order to enable Azure AD users to log into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="38d1e-209">In the case of FreshDesk, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="38d1e-209">In the case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="38d1e-210">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="38d1e-210">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="38d1e-211">Log in to your **Freshdesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="38d1e-211">Log in to your **Freshdesk** tenant.</span></span>
2. <span data-ttu-id="38d1e-212">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-212">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="38d1e-213">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="38d1e-213">![Admin](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="38d1e-214">In the **General Settings** tab, click **Agents**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-214">In the **General Settings** tab, click **Agents**.</span></span>
   
    <span data-ttu-id="38d1e-215">![Agents](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span><span class="sxs-lookup"><span data-stu-id="38d1e-215">![Agents](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="38d1e-216">Click **New Agent**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-216">Click **New Agent**.</span></span>
   
    <span data-ttu-id="38d1e-217">![New Agent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span><span class="sxs-lookup"><span data-stu-id="38d1e-217">![New Agent](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="38d1e-218">On the Agent Information dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="38d1e-218">On the Agent Information dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="38d1e-219">![Agent Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span><span class="sxs-lookup"><span data-stu-id="38d1e-219">![Agent Information](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/IC776775.png "Agent Information")</span></span>
   
    <span data-ttu-id="38d1e-220">a.</span><span class="sxs-lookup"><span data-stu-id="38d1e-220">a.</span></span> <span data-ttu-id="38d1e-221">In the **Full Name** textbox, type the name of the Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="38d1e-221">In the **Full Name** textbox, type the name of the Azure AD account you want to provision.</span></span>

    <span data-ttu-id="38d1e-222">b.</span><span class="sxs-lookup"><span data-stu-id="38d1e-222">b.</span></span> <span data-ttu-id="38d1e-223">In the **Email** textbox, type the Azure AD email address of the Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="38d1e-223">In the **Email** textbox, type the Azure AD email address of the Azure AD account you want to provision.</span></span>

    <span data-ttu-id="38d1e-224">c.</span><span class="sxs-lookup"><span data-stu-id="38d1e-224">c.</span></span> <span data-ttu-id="38d1e-225">In the **Title** textbox, type the title of the Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="38d1e-225">In the **Title** textbox, type the title of the Azure AD account you want to provision.</span></span>

    <span data-ttu-id="38d1e-226">d.</span><span class="sxs-lookup"><span data-stu-id="38d1e-226">d.</span></span> <span data-ttu-id="38d1e-227">Select **Agents role**, and then click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-227">Select **Agents role**, and then click **Assign**.</span></span>
       
    <span data-ttu-id="38d1e-228">e.</span><span class="sxs-lookup"><span data-stu-id="38d1e-228">e.</span></span> <span data-ttu-id="38d1e-229">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-229">Click **Save**.</span></span>     
   
    >[!NOTE]
    ><span data-ttu-id="38d1e-230">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span><span class="sxs-lookup"><span data-stu-id="38d1e-230">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span></span> 
    > 
    
    >[!NOTE]
    ><span data-ttu-id="38d1e-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="38d1e-231">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk to provision AAD user accounts.</span></span> <span data-ttu-id="38d1e-232">to FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="38d1e-232">to FreshDesk.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="38d1e-233">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="38d1e-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="38d1e-234">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Box.</span><span class="sxs-lookup"><span data-stu-id="38d1e-234">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Box.</span></span>

![Assign User][200] 

<span data-ttu-id="38d1e-236">**To assign Britta Simon to FreshDesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="38d1e-236">**To assign Britta Simon to FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="38d1e-237">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-237">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="38d1e-239">In the applications list, select **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-239">In the applications list, select **FreshDesk**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="38d1e-241">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="38d1e-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="38d1e-243">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="38d1e-243">Click **Add** button.</span></span> <span data-ttu-id="38d1e-244">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="38d1e-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="38d1e-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="38d1e-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="38d1e-247">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="38d1e-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38d1e-248">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="38d1e-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="38d1e-249">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="38d1e-249">Testing single sign-on</span></span>

<span data-ttu-id="38d1e-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="38d1e-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="38d1e-251">When you click the FreshDesk tile in the Access Panel, you should get login page to get signed-on to your FreshDesk application.</span><span class="sxs-lookup"><span data-stu-id="38d1e-251">When you click the FreshDesk tile in the Access Panel, you should get login page to get signed-on to your FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="38d1e-252">Additional resources</span><span class="sxs-lookup"><span data-stu-id="38d1e-252">Additional resources</span></span>

* [<span data-ttu-id="38d1e-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38d1e-253">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38d1e-254">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="38d1e-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-freshdesk-tutorial/tutorial_general_203.png





























