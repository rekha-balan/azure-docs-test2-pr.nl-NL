---
title: 'Tutorial: Azure Active Directory integration with TeamSeer | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TeamSeer.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 6ec4806f-fe0f-4ed7-8cfa-32d1c840433f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: a5910689f34c511c6cf7d8a044ef4358d2e0570d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868349"
---
# <a name="tutorial-azure-active-directory-integration-with-teamseer"></a><span data-ttu-id="0c4eb-103">Tutorial: Azure Active Directory integration with TeamSeer</span><span class="sxs-lookup"><span data-stu-id="0c4eb-103">Tutorial: Azure Active Directory integration with TeamSeer</span></span>

<span data-ttu-id="0c4eb-104">In this tutorial, you learn how to integrate TeamSeer with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0c4eb-104">In this tutorial, you learn how to integrate TeamSeer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0c4eb-105">Integrating TeamSeer with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="0c4eb-105">Integrating TeamSeer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0c4eb-106">You can control in Azure AD who has access to TeamSeer</span><span class="sxs-lookup"><span data-stu-id="0c4eb-106">You can control in Azure AD who has access to TeamSeer</span></span>
- <span data-ttu-id="0c4eb-107">You can enable your users to automatically get signed-on to TeamSeer (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="0c4eb-107">You can enable your users to automatically get signed-on to TeamSeer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0c4eb-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0c4eb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0c4eb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="0c4eb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c4eb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0c4eb-110">Prerequisites</span></span>

<span data-ttu-id="0c4eb-111">To configure Azure AD integration with TeamSeer, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="0c4eb-111">To configure Azure AD integration with TeamSeer, you need the following items:</span></span>

- <span data-ttu-id="0c4eb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="0c4eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0c4eb-113">A TeamSeer single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="0c4eb-113">A TeamSeer single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0c4eb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0c4eb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="0c4eb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0c4eb-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0c4eb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c4eb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0c4eb-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="0c4eb-118">Scenario description</span></span>
<span data-ttu-id="0c4eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0c4eb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="0c4eb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0c4eb-121">Adding TeamSeer from the gallery</span><span class="sxs-lookup"><span data-stu-id="0c4eb-121">Adding TeamSeer from the gallery</span></span>
1. <span data-ttu-id="0c4eb-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0c4eb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamseer-from-the-gallery"></a><span data-ttu-id="0c4eb-123">Adding TeamSeer from the gallery</span><span class="sxs-lookup"><span data-stu-id="0c4eb-123">Adding TeamSeer from the gallery</span></span>
<span data-ttu-id="0c4eb-124">To configure the integration of TeamSeer in to Azure AD, you need to add TeamSeer from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-124">To configure the integration of TeamSeer in to Azure AD, you need to add TeamSeer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0c4eb-125">**To add TeamSeer from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0c4eb-125">**To add TeamSeer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0c4eb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="0c4eb-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0c4eb-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="0c4eb-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="0c4eb-133">In the search box, type **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-133">In the search box, type **TeamSeer**.</span></span>

    ![Creating an Azure AD test user](./media/teamseer-tutorial/tutorial_teamseer_search.png)

1. <span data-ttu-id="0c4eb-135">In the results panel, select **TeamSeer**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-135">In the results panel, select **TeamSeer**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/teamseer-tutorial/tutorial_teamseer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0c4eb-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0c4eb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0c4eb-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="0c4eb-138">In this section, you configure and test Azure AD single sign-on with TeamSeer based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0c4eb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TeamSeer is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TeamSeer is to a user in Azure AD.</span></span> <span data-ttu-id="0c4eb-140">In other words, a link relationship between an Azure AD user and the related user in TeamSeer needs to be established.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-140">In other words, a link relationship between an Azure AD user and the related user in TeamSeer needs to be established.</span></span>

<span data-ttu-id="0c4eb-141">In TeamSeer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-141">In TeamSeer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0c4eb-142">To configure and test Azure AD single sign-on with TeamSeer, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="0c4eb-142">To configure and test Azure AD single sign-on with TeamSeer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0c4eb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="0c4eb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="0c4eb-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - to have a counterpart of Britta Simon in TeamSeer that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-145">**[Creating a TeamSeer test user](#creating-a-teamseer-test-user)** - to have a counterpart of Britta Simon in TeamSeer that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="0c4eb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="0c4eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0c4eb-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="0c4eb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0c4eb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TeamSeer application.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TeamSeer application.</span></span>

<span data-ttu-id="0c4eb-150">**To configure Azure AD single sign-on with TeamSeer, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0c4eb-150">**To configure Azure AD single sign-on with TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="0c4eb-151">In the Azure portal, on the **TeamSeer** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-151">In the Azure portal, on the **TeamSeer** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="0c4eb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/teamseer-tutorial/tutorial_teamseer_samlbase.png)

1. <span data-ttu-id="0c4eb-155">On the **TeamSeer Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c4eb-155">On the **TeamSeer Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/teamseer-tutorial/tutorial_teamseer_url.png)

     <span data-ttu-id="0c4eb-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.teamseer.com/<companyid>`</span><span class="sxs-lookup"><span data-stu-id="0c4eb-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.teamseer.com/<companyid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0c4eb-158">The value is not real.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-158">The value is not real.</span></span> <span data-ttu-id="0c4eb-159">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="0c4eb-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) to get the value.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-160">Contact [TeamSeer Client support team](http://pages.theaccessgroup.com/solutions_business-suite_absence-management_contact.html) to get the value.</span></span> 
 
1. <span data-ttu-id="0c4eb-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/teamseer-tutorial/tutorial_teamseer_certificate.png) 

1. <span data-ttu-id="0c4eb-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/teamseer-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="0c4eb-165">On the **TeamSeer Configuration** section, click **Configure TeamSeer** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-165">On the **TeamSeer Configuration** section, click **Configure TeamSeer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0c4eb-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="0c4eb-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/teamseer-tutorial/tutorial_teamseer_configure.png)

1. <span data-ttu-id="0c4eb-168">In a different web browser window, log in to your TeamSeer company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-168">In a different web browser window, log in to your TeamSeer company site as an administrator.</span></span>

1. <span data-ttu-id="0c4eb-169">Go to **HR Admin**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-169">Go to **HR Admin**.</span></span>
   
    <span data-ttu-id="0c4eb-170">![HR Admin](./media/teamseer-tutorial/ic789634.png "HR Admin")</span><span class="sxs-lookup"><span data-stu-id="0c4eb-170">![HR Admin](./media/teamseer-tutorial/ic789634.png "HR Admin")</span></span>

1. <span data-ttu-id="0c4eb-171">Click **Setup**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-171">Click **Setup**.</span></span>
   
    <span data-ttu-id="0c4eb-172">![Setup](./media/teamseer-tutorial/ic789635.png "Setup")</span><span class="sxs-lookup"><span data-stu-id="0c4eb-172">![Setup](./media/teamseer-tutorial/ic789635.png "Setup")</span></span>

1. <span data-ttu-id="0c4eb-173">Click **Set up SAML provider details**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-173">Click **Set up SAML provider details**.</span></span>
   
    <span data-ttu-id="0c4eb-174">![SAML Settings](./media/teamseer-tutorial/ic789636.png "SAML Settings")</span><span class="sxs-lookup"><span data-stu-id="0c4eb-174">![SAML Settings](./media/teamseer-tutorial/ic789636.png "SAML Settings")</span></span>

1. <span data-ttu-id="0c4eb-175">In the SAML provider details section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c4eb-175">In the SAML provider details section, perform the following steps:</span></span>
   
    <span data-ttu-id="0c4eb-176">![SAML Settings](./media/teamseer-tutorial/ic789637.png "SAML Settings")</span><span class="sxs-lookup"><span data-stu-id="0c4eb-176">![SAML Settings](./media/teamseer-tutorial/ic789637.png "SAML Settings")</span></span>   

    <span data-ttu-id="0c4eb-177">a.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-177">a.</span></span> <span data-ttu-id="0c4eb-178">Paste the **Single Sign-On Service URL** value in to the **URL** textbox.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-178">Paste the **Single Sign-On Service URL** value in to the **URL** textbox.</span></span>
          
    <span data-ttu-id="0c4eb-179">b.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-179">b.</span></span> <span data-ttu-id="0c4eb-180">Open your base-64 encoded certificate in notepad, copy the content of it in to your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-180">Open your base-64 encoded certificate in notepad, copy the content of it in to your clipboard, and then paste it to the **IdP Public Certificate** textbox.</span></span>

1. <span data-ttu-id="0c4eb-181">To complete the SAML provider configuration, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c4eb-181">To complete the SAML provider configuration, perform the following steps:</span></span>
    
    <span data-ttu-id="0c4eb-182">![SAML Settings](./media/teamseer-tutorial/ic789638.png "SAML Settings")</span><span class="sxs-lookup"><span data-stu-id="0c4eb-182">![SAML Settings](./media/teamseer-tutorial/ic789638.png "SAML Settings")</span></span> 

    <span data-ttu-id="0c4eb-183">a.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-183">a.</span></span> <span data-ttu-id="0c4eb-184">In the **Test Email Addresses**, type the test user’s email address.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-184">In the **Test Email Addresses**, type the test user’s email address.</span></span> 
  
    <span data-ttu-id="0c4eb-185">b.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-185">b.</span></span> <span data-ttu-id="0c4eb-186">In the **Issuer** textbox, type the Issuer URL of the service provider.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-186">In the **Issuer** textbox, type the Issuer URL of the service provider.</span></span> 
  
    <span data-ttu-id="0c4eb-187">c.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-187">c.</span></span> <span data-ttu-id="0c4eb-188">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0c4eb-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="0c4eb-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0c4eb-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0c4eb-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0c4eb-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0c4eb-192">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0c4eb-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="0c4eb-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="0c4eb-195">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0c4eb-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0c4eb-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/teamseer-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="0c4eb-198">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/teamseer-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="0c4eb-200">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/teamseer-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="0c4eb-202">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c4eb-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/teamseer-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0c4eb-204">a.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-204">a.</span></span> <span data-ttu-id="0c4eb-205">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0c4eb-206">b.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-206">b.</span></span> <span data-ttu-id="0c4eb-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0c4eb-208">c.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-208">c.</span></span> <span data-ttu-id="0c4eb-209">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0c4eb-210">d.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-210">d.</span></span> <span data-ttu-id="0c4eb-211">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-211">Click **Create**.</span></span>
 
### <a name="creating-a-teamseer-test-user"></a><span data-ttu-id="0c4eb-212">Creating a TeamSeer test user</span><span class="sxs-lookup"><span data-stu-id="0c4eb-212">Creating a TeamSeer test user</span></span>

<span data-ttu-id="0c4eb-213">To enable Azure AD users to log in to TeamSeer, they must be provisioned in to ShiftPlanning.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-213">To enable Azure AD users to log in to TeamSeer, they must be provisioned in to ShiftPlanning.</span></span> <span data-ttu-id="0c4eb-214">In the case of TeamSeer, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-214">In the case of TeamSeer, provisioning is a manual task.</span></span>

<span data-ttu-id="0c4eb-215">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0c4eb-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="0c4eb-216">Log in to your **TeamSeer** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-216">Log in to your **TeamSeer** company site as an administrator.</span></span>

1. <span data-ttu-id="0c4eb-217">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c4eb-217">Perform the following steps:</span></span>
   
    <span data-ttu-id="0c4eb-218">![HR Admin](./media/teamseer-tutorial/ic789640.png "HR Admin")</span><span class="sxs-lookup"><span data-stu-id="0c4eb-218">![HR Admin](./media/teamseer-tutorial/ic789640.png "HR Admin")</span></span>  
 
    <span data-ttu-id="0c4eb-219">a.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-219">a.</span></span> <span data-ttu-id="0c4eb-220">Go to **HR Admin \> Users**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-220">Go to **HR Admin \> Users**.</span></span>
  
    <span data-ttu-id="0c4eb-221">b.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-221">b.</span></span> <span data-ttu-id="0c4eb-222">Click **Run the New User wizard**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-222">Click **Run the New User wizard**.</span></span>

1. <span data-ttu-id="0c4eb-223">In the **User Details** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c4eb-223">In the **User Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="0c4eb-224">![User Details](./media/teamseer-tutorial/ic789641.png "User Details")</span><span class="sxs-lookup"><span data-stu-id="0c4eb-224">![User Details](./media/teamseer-tutorial/ic789641.png "User Details")</span></span>

    <span data-ttu-id="0c4eb-225">a.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-225">a.</span></span> <span data-ttu-id="0c4eb-226">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision in to the related textboxes.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-226">Type the **First Name**, **Surname**, **User name (Email address)** of a valid AAD account you want to provision in to the related textboxes.</span></span>
  
    <span data-ttu-id="0c4eb-227">b.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-227">b.</span></span> <span data-ttu-id="0c4eb-228">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-228">Click **Next**.</span></span>

1. <span data-ttu-id="0c4eb-229">Follow the on-screen instructions for adding a new user, and click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-229">Follow the on-screen instructions for adding a new user, and click **Finish**.</span></span>

>[!NOTE]
><span data-ttu-id="0c4eb-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-230">You can use any other TeamSeer user account creation tools or APIs provided by TeamSeer to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0c4eb-231">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="0c4eb-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0c4eb-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TeamSeer.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TeamSeer.</span></span>

![Assign User][200] 

<span data-ttu-id="0c4eb-234">**To assign Britta Simon to TeamSeer, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="0c4eb-234">**To assign Britta Simon to TeamSeer, perform the following steps:**</span></span>

1. <span data-ttu-id="0c4eb-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="0c4eb-237">In the applications list, select **TeamSeer**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-237">In the applications list, select **TeamSeer**.</span></span>

    ![Configure Single Sign-On](./media/teamseer-tutorial/tutorial_teamseer_app.png) 

1. <span data-ttu-id="0c4eb-239">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="0c4eb-241">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-241">Click **Add** button.</span></span> <span data-ttu-id="0c4eb-242">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="0c4eb-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="0c4eb-245">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-245">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="0c4eb-246">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0c4eb-247">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="0c4eb-247">Testing single sign-on</span></span>

<span data-ttu-id="0c4eb-248">If you want to test your single sign-on settings, open the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="0c4eb-248">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="0c4eb-249">For more details about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0c4eb-249">For more details about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0c4eb-250">Additional resources</span><span class="sxs-lookup"><span data-stu-id="0c4eb-250">Additional resources</span></span>

* [<span data-ttu-id="0c4eb-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c4eb-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="0c4eb-252">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0c4eb-252">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/teamseer-tutorial/tutorial_general_01.png
[2]: ./media/teamseer-tutorial/tutorial_general_02.png
[3]: ./media/teamseer-tutorial/tutorial_general_03.png
[4]: ./media/teamseer-tutorial/tutorial_general_04.png

[100]: ./media/teamseer-tutorial/tutorial_general_100.png

[200]: ./media/teamseer-tutorial/tutorial_general_200.png
[201]: ./media/teamseer-tutorial/tutorial_general_201.png
[202]: ./media/teamseer-tutorial/tutorial_general_202.png
[203]: ./media/teamseer-tutorial/tutorial_general_203.png

