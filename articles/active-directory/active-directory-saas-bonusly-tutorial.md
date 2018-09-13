---
title: 'Tutorial: Azure Active Directory integration with Bonusly | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Bonusly.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 42875d53-0769-4520-a6af-7308b5240d6b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/07/2017
ms.author: jeedes
ms.openlocfilehash: 24f9a1ca1a88cd4491c1b0062b8d754d4a694a41
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563901"
---
# <a name="tutorial-azure-active-directory-integration-with-bonusly"></a><span data-ttu-id="5b9e5-103">Tutorial: Azure Active Directory integration with Bonusly</span><span class="sxs-lookup"><span data-stu-id="5b9e5-103">Tutorial: Azure Active Directory integration with Bonusly</span></span>

<span data-ttu-id="5b9e5-104">In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5b9e5-104">In this tutorial, you learn how to integrate Bonusly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5b9e5-105">Integrating Bonusly with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="5b9e5-105">Integrating Bonusly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5b9e5-106">You can control in Azure AD who has access to Bonusly</span><span class="sxs-lookup"><span data-stu-id="5b9e5-106">You can control in Azure AD who has access to Bonusly</span></span>
- <span data-ttu-id="5b9e5-107">You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="5b9e5-107">You can enable your users to automatically get signed-on to Bonusly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5b9e5-108">You can manage your accounts in one central location - the Azure Management portal</span><span class="sxs-lookup"><span data-stu-id="5b9e5-108">You can manage your accounts in one central location - the Azure Management portal</span></span>

<span data-ttu-id="5b9e5-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5b9e5-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b9e5-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5b9e5-110">Prerequisites</span></span>

<span data-ttu-id="5b9e5-111">To configure Azure AD integration with Bonusly, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="5b9e5-111">To configure Azure AD integration with Bonusly, you need the following items:</span></span>

- <span data-ttu-id="5b9e5-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="5b9e5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5b9e5-113">A Bonusly single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="5b9e5-113">A Bonusly single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="5b9e5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="5b9e5-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="5b9e5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5b9e5-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="5b9e5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5b9e5-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="5b9e5-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="5b9e5-118">Scenario description</span></span>
<span data-ttu-id="5b9e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5b9e5-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="5b9e5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5b9e5-121">Adding Bonusly from the gallery</span><span class="sxs-lookup"><span data-stu-id="5b9e5-121">Adding Bonusly from the gallery</span></span>
2. <span data-ttu-id="5b9e5-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b9e5-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-bonusly-from-the-gallery"></a><span data-ttu-id="5b9e5-123">Adding Bonusly from the gallery</span><span class="sxs-lookup"><span data-stu-id="5b9e5-123">Adding Bonusly from the gallery</span></span>
<span data-ttu-id="5b9e5-124">To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-124">To configure the integration of Bonusly into Azure AD, you need to add Bonusly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5b9e5-125">**To add Bonusly from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b9e5-125">**To add Bonusly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5b9e5-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-126">In the **[Azure Management Portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5b9e5-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5b9e5-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5b9e5-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5b9e5-133">In the search box, type **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-133">In the search box, type **Bonusly**.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_001.png)

5. <span data-ttu-id="5b9e5-135">In the results panel, select **Bonusly**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-135">In the results panel, select **Bonusly**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5b9e5-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b9e5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5b9e5-138">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="5b9e5-138">In this section, you configure and test Azure AD single sign-on with Bonusly based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5b9e5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Bonusly is to a user in Azure AD.</span></span> <span data-ttu-id="5b9e5-140">In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-140">In other words, a link relationship between an Azure AD user and the related user in Bonusly needs to be established.</span></span>

<span data-ttu-id="5b9e5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bonusly.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bonusly.</span></span>

<span data-ttu-id="5b9e5-142">To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="5b9e5-142">To configure and test Azure AD single sign-on with Bonusly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5b9e5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5b9e5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5b9e5-145">**[Creating a Bonusly test user](#creating-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-145">**[Creating a Bonusly test user](#creating-a-bonusly-test-user)** - to have a counterpart of Britta Simon in Bonusly that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="5b9e5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5b9e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5b9e5-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b9e5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5b9e5-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Bonusly application.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-149">In this section, you enable Azure AD single sign-on in the Azure Management portal and configure single sign-on in your Bonusly application.</span></span>

<span data-ttu-id="5b9e5-150">**To configure Azure AD single sign-on with Bonusly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b9e5-150">**To configure Azure AD single sign-on with Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="5b9e5-151">In the Azure Management portal, on the **Bonusly** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-151">In the Azure Management portal, on the **Bonusly** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="5b9e5-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-153">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>
 
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_01.png)

3. <span data-ttu-id="5b9e5-155">On the **Bonusly Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5b9e5-155">On the **Bonusly Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_02.png)

    <span data-ttu-id="5b9e5-157">a.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-157">a.</span></span> <span data-ttu-id="5b9e5-158">In the **Identifier** textbox, type the value as: `bonusly`</span><span class="sxs-lookup"><span data-stu-id="5b9e5-158">In the **Identifier** textbox, type the value as: `bonusly`</span></span>
    
    <span data-ttu-id="5b9e5-159">b.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-159">b.</span></span> <span data-ttu-id="5b9e5-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://bonus.ly/saml/<APP-ID>/consume`</span><span class="sxs-lookup"><span data-stu-id="5b9e5-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://bonus.ly/saml/<APP-ID>/consume`</span></span>
    
4. <span data-ttu-id="5b9e5-161">If you wish to configure the application in **SP initiated mode**, on the **Bonusly Domain and URLs** section perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5b9e5-161">If you wish to configure the application in **SP initiated mode**, on the **Bonusly Domain and URLs** section perform the following steps:</span></span>
    
    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_03.png)

    <span data-ttu-id="5b9e5-163">a.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-163">a.</span></span> <span data-ttu-id="5b9e5-164">Click on the **Show advanced URL settings** option</span><span class="sxs-lookup"><span data-stu-id="5b9e5-164">Click on the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="5b9e5-165">b.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-165">b.</span></span> <span data-ttu-id="5b9e5-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://bonus.ly/saml/<your_subdomain>/consume`</span><span class="sxs-lookup"><span data-stu-id="5b9e5-166">In the **Sign On URL** textbox, type a URL using the following pattern: `https://bonus.ly/saml/<your_subdomain>/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b9e5-167">Please note that these are not the real values.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-167">Please note that these are not the real values.</span></span> <span data-ttu-id="5b9e5-168">You have to update these values with the actual Sign On URL, Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-168">You have to update these values with the actual Sign On URL, Identifier and Reply URL.</span></span> <span data-ttu-id="5b9e5-169">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-169">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="5b9e5-170">Contact [Bonusly support team](mailto:sales@easyterritory.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-170">Contact [Bonusly support team](mailto:sales@easyterritory.com) to get these values.</span></span>

5. <span data-ttu-id="5b9e5-171">On the **SAML Signing Certificate** section, click **Create new certificate**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-171">On the **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_04.png)    

6. <span data-ttu-id="5b9e5-173">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-173">On the **Create New Certificate** dialog, click the calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="5b9e5-174">Then click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-174">Then click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_300.png)

7. <span data-ttu-id="5b9e5-176">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-176">On the **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_05.png)

8. <span data-ttu-id="5b9e5-178">On the pop-up **Rollover certificate** window, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-178">On the pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="5b9e5-180">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-180">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_06.png) 

10. <span data-ttu-id="5b9e5-182">On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-182">On the **Bonusly Configuration** section, click **Configure Bonusly** to open **Configure sign-on** window.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_07.png) 

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_08.png)

11. <span data-ttu-id="5b9e5-185">In a different web browser window, log into your Bonusly company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-185">In a different web browser window, log into your Bonusly company site as an administrator.</span></span>

12. <span data-ttu-id="5b9e5-186">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-186">In the toolbar on the top, click **Settings**, and then select **Integrations and apps**.</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_002.png)

13. <span data-ttu-id="5b9e5-188">Under **Single Sign-On**, select **SAML**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-188">Under **Single Sign-On**, select **SAML**.</span></span>

14. <span data-ttu-id="5b9e5-189">On the **SAML** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5b9e5-189">On the **SAML** dialog page, perform the following steps:</span></span>

    ![Configure Single Sign-On On App Side](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_003.png)

    <span data-ttu-id="5b9e5-191">a.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-191">a.</span></span> <span data-ttu-id="5b9e5-192">In the **IdP SSO target URL** textbox put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-192">In the **IdP SSO target URL** textbox put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="5b9e5-193">b.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-193">b.</span></span> <span data-ttu-id="5b9e5-194">In the **IdP Login URL** textbox put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-194">In the **IdP Login URL** textbox put the value of **SAML Single Sign-On Service URL** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="5b9e5-195">c.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-195">c.</span></span> <span data-ttu-id="5b9e5-196">In the **IdP Issuer** textbox put the value of **SAML Entity ID** from Azure AD application configuration window.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-196">In the **IdP Issuer** textbox put the value of **SAML Entity ID** from Azure AD application configuration window.</span></span>

    <span data-ttu-id="5b9e5-197">d.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-197">d.</span></span> <span data-ttu-id="5b9e5-198">Copy the thumbprint value from the downloaded certificate, and then paste it into the **Cert Fingerprint** textbox.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-198">Copy the thumbprint value from the downloaded certificate, and then paste it into the **Cert Fingerprint** textbox.</span></span>

    <span data-ttu-id="5b9e5-199">e.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-199">e.</span></span> <span data-ttu-id="5b9e5-200">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-200">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b9e5-201">For more details, see [How to retrieve a certificate's thumbprint value](https://www.youtube.com/watch?v=YKQF266SAxI&feature=youtu.be).</span><span class="sxs-lookup"><span data-stu-id="5b9e5-201">For more details, see [How to retrieve a certificate's thumbprint value](https://www.youtube.com/watch?v=YKQF266SAxI&feature=youtu.be).</span></span>



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5b9e5-202">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5b9e5-202">Creating an Azure AD test user</span></span>
<span data-ttu-id="5b9e5-203">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-203">The objective of this section is to create a test user in the Azure Management portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="5b9e5-205">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b9e5-205">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5b9e5-206">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-206">In the **Azure Management portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5b9e5-208">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-208">Go to **Users and groups** and click **All users** to display the list of users.</span></span>
    
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5b9e5-210">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-210">At the top of the dialog click **Add** to open the **User** dialog.</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5b9e5-212">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5b9e5-212">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5b9e5-214">a.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-214">a.</span></span> <span data-ttu-id="5b9e5-215">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-215">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5b9e5-216">b.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-216">b.</span></span> <span data-ttu-id="5b9e5-217">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-217">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5b9e5-218">c.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-218">c.</span></span> <span data-ttu-id="5b9e5-219">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-219">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5b9e5-220">d.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-220">d.</span></span> <span data-ttu-id="5b9e5-221">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-221">Click **Create**.</span></span> 



### <a name="creating-a-bonusly-test-user"></a><span data-ttu-id="5b9e5-222">Creating a Bonusly test user</span><span class="sxs-lookup"><span data-stu-id="5b9e5-222">Creating a Bonusly test user</span></span>

<span data-ttu-id="5b9e5-223">In order to enable Azure AD users to log into Bonusly, they must be provisioned into Bonusly.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-223">In order to enable Azure AD users to log into Bonusly, they must be provisioned into Bonusly.</span></span>
<span data-ttu-id="5b9e5-224">In the case of Bonusly, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-224">In the case of Bonusly, provisioning is a manual task.</span></span>

####<a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="5b9e5-225">To provision a user account, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5b9e5-225">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="5b9e5-226">Log into your Bonusly company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-226">Log into your Bonusly company site as an administrator.</span></span>

2. <span data-ttu-id="5b9e5-227">Click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-227">Click **Settings**.</span></span>

    <span data-ttu-id="5b9e5-228">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_010.png "New User")</span><span class="sxs-lookup"><span data-stu-id="5b9e5-228">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_010.png "New User")</span></span>

3. <span data-ttu-id="5b9e5-229">Click the **Users and bonuses** tab.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-229">Click the **Users and bonuses** tab.</span></span>

    <span data-ttu-id="5b9e5-230">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_011.png "New User")</span><span class="sxs-lookup"><span data-stu-id="5b9e5-230">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_011.png "New User")</span></span>

4. <span data-ttu-id="5b9e5-231">Click **Manage Users**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-231">Click **Manage Users**.</span></span>

    <span data-ttu-id="5b9e5-232">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_012.png "New User")</span><span class="sxs-lookup"><span data-stu-id="5b9e5-232">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_012.png "New User")</span></span>

5. <span data-ttu-id="5b9e5-233">Click **Add User**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-233">Click **Add User**.</span></span>

    <span data-ttu-id="5b9e5-234">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_013.png "New User")</span><span class="sxs-lookup"><span data-stu-id="5b9e5-234">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_013.png "New User")</span></span>

6. <span data-ttu-id="5b9e5-235">In the **Add User** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5b9e5-235">In the **Add User** section, perform the following steps:</span></span>

    <span data-ttu-id="5b9e5-236">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_014.png "New User")</span><span class="sxs-lookup"><span data-stu-id="5b9e5-236">![New User](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_014.png "New User")</span></span>

    <span data-ttu-id="5b9e5-237">a.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-237">a.</span></span> <span data-ttu-id="5b9e5-238">In the **First Name** textbox, type **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-238">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="5b9e5-239">b.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-239">b.</span></span> <span data-ttu-id="5b9e5-240">In the **Last Name** textbox, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-240">In the **Last Name** textbox, type **Simon**.</span></span>

    <span data-ttu-id="5b9e5-241">c.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-241">c.</span></span> <span data-ttu-id="5b9e5-242">In the **Email** textbox, type the email address of Britta Simon account.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-242">In the **Email** textbox, type the email address of Britta Simon account.</span></span>

    <span data-ttu-id="5b9e5-243">d.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-243">d.</span></span> <span data-ttu-id="5b9e5-244">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-244">Click **Save**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5b9e5-245">The AAD account holder will receive an email that includes a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-245">The AAD account holder will receive an email that includes a link to confirm the account before it becomes active.</span></span> <span data-ttu-id="5b9e5-246">You can use any other Bonus.ly user account creation tools or APIs provided by Bonus.ly to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-246">You can use any other Bonus.ly user account creation tools or APIs provided by Bonus.ly to provision AAD user accounts.</span></span>



### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5b9e5-247">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="5b9e5-247">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5b9e5-248">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bonusly.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-248">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Bonusly.</span></span>

![Assign User][200] 

<span data-ttu-id="5b9e5-250">**To assign Britta Simon to Bonusly, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="5b9e5-250">**To assign Britta Simon to Bonusly, perform the following steps:**</span></span>

1. <span data-ttu-id="5b9e5-251">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-251">In the Azure Management portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

2. <span data-ttu-id="5b9e5-253">In the applications list, select **Bonusly**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-253">In the applications list, select **Bonusly**.</span></span>

    ![Configure Single Sign-On](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_bonusly_50.png) 

3. <span data-ttu-id="5b9e5-255">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-255">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

4. <span data-ttu-id="5b9e5-257">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-257">Click **Add** button.</span></span> <span data-ttu-id="5b9e5-258">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-258">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="5b9e5-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-260">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5b9e5-261">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-261">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5b9e5-262">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-262">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="5b9e5-263">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="5b9e5-263">Testing single sign-on</span></span>

<span data-ttu-id="5b9e5-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-264">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5b9e5-265">When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.</span><span class="sxs-lookup"><span data-stu-id="5b9e5-265">When you click the Bonusly tile in the Access Panel, you should get automatically signed-on to your Bonusly application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="5b9e5-266">Additional resources</span><span class="sxs-lookup"><span data-stu-id="5b9e5-266">Additional resources</span></span>

* [<span data-ttu-id="5b9e5-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b9e5-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5b9e5-268">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5b9e5-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_01.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_02.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_03.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_04.png

[100]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_100.png

[200]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_200.png
[201]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_201.png
[202]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_202.png
[203]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-bonusly-tutorial/tutorial_general_203.png
































