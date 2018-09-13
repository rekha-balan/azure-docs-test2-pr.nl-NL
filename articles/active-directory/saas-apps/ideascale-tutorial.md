---
title: 'Tutorial: Azure Active Directory integration with IdeaScale | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and IdeaScale.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1f6c2c9b01a2f861214240eca054242ec73f3929
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856451"
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="a5553-103">Tutorial: Azure Active Directory integration with IdeaScale</span><span class="sxs-lookup"><span data-stu-id="a5553-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="a5553-104">In this tutorial, you learn how to integrate IdeaScale with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a5553-104">In this tutorial, you learn how to integrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a5553-105">Integrating IdeaScale with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a5553-105">Integrating IdeaScale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a5553-106">You can control in Azure AD who has access to IdeaScale</span><span class="sxs-lookup"><span data-stu-id="a5553-106">You can control in Azure AD who has access to IdeaScale</span></span>
- <span data-ttu-id="a5553-107">You can enable your users to automatically get signed-on to IdeaScale (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="a5553-107">You can enable your users to automatically get signed-on to IdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a5553-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="a5553-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a5553-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="a5553-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5553-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a5553-110">Prerequisites</span></span>

<span data-ttu-id="a5553-111">To configure Azure AD integration with IdeaScale, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="a5553-111">To configure Azure AD integration with IdeaScale, you need the following items:</span></span>

- <span data-ttu-id="a5553-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="a5553-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a5553-113">An IdeaScale single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="a5553-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a5553-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="a5553-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a5553-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="a5553-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a5553-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="a5553-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a5553-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a5553-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a5553-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="a5553-118">Scenario description</span></span>
<span data-ttu-id="a5553-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="a5553-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a5553-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="a5553-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a5553-121">Adding IdeaScale from the gallery</span><span class="sxs-lookup"><span data-stu-id="a5553-121">Adding IdeaScale from the gallery</span></span>
1. <span data-ttu-id="a5553-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5553-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-the-gallery"></a><span data-ttu-id="a5553-123">Adding IdeaScale from the gallery</span><span class="sxs-lookup"><span data-stu-id="a5553-123">Adding IdeaScale from the gallery</span></span>
<span data-ttu-id="a5553-124">To configure the integration of IdeaScale into Azure AD, you need to add IdeaScale from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="a5553-124">To configure the integration of IdeaScale into Azure AD, you need to add IdeaScale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a5553-125">**To add IdeaScale from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5553-125">**To add IdeaScale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a5553-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a5553-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="a5553-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="a5553-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a5553-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a5553-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="a5553-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="a5553-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="a5553-133">In the search box, type **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="a5553-133">In the search box, type **IdeaScale**.</span></span>

    ![Creating an Azure AD test user](./media/ideascale-tutorial/tutorial_ideascale_search.png)

1. <span data-ttu-id="a5553-135">In the results panel, select **IdeaScale**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="a5553-135">In the results panel, select **IdeaScale**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a5553-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5553-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a5553-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="a5553-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a5553-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IdeaScale is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a5553-139">For single sign-on to work, Azure AD needs to know what the counterpart user in IdeaScale is to a user in Azure AD.</span></span> <span data-ttu-id="a5553-140">In other words, a link relationship between an Azure AD user and the related user in IdeaScale needs to be established.</span><span class="sxs-lookup"><span data-stu-id="a5553-140">In other words, a link relationship between an Azure AD user and the related user in IdeaScale needs to be established.</span></span>

<span data-ttu-id="a5553-141">In IdeaScale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="a5553-141">In IdeaScale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a5553-142">To configure and test Azure AD single sign-on with IdeaScale, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="a5553-142">To configure and test Azure AD single sign-on with IdeaScale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a5553-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="a5553-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="a5553-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5553-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="a5553-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - to have a counterpart of Britta Simon in IdeaScale that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="a5553-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - to have a counterpart of Britta Simon in IdeaScale that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="a5553-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a5553-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="a5553-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="a5553-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a5553-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5553-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a5553-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IdeaScale application.</span><span class="sxs-lookup"><span data-stu-id="a5553-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="a5553-150">**To configure Azure AD single sign-on with IdeaScale, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5553-150">**To configure Azure AD single sign-on with IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="a5553-151">In the Azure portal, on the **IdeaScale** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="a5553-151">In the Azure portal, on the **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="a5553-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a5553-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/ideascale-tutorial/tutorial_ideascale_samlbase.png)

1. <span data-ttu-id="a5553-155">On the **IdeaScale Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a5553-155">On the **IdeaScale Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="a5553-157">a.</span><span class="sxs-lookup"><span data-stu-id="a5553-157">a.</span></span> <span data-ttu-id="a5553-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="a5553-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="a5553-159">b.</span><span class="sxs-lookup"><span data-stu-id="a5553-159">b.</span></span> <span data-ttu-id="a5553-160">In the **Identifier** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="a5553-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="a5553-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="a5553-161">These values are not real.</span></span> <span data-ttu-id="a5553-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="a5553-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a5553-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="a5553-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) to get these values.</span></span> 
 
1. <span data-ttu-id="a5553-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="a5553-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/ideascale-tutorial/tutorial_ideascale_certificate.png) 

1. <span data-ttu-id="a5553-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="a5553-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/ideascale-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="a5553-168">On the **IdeaScale Configuration** section, click **Configure IdeaScale** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="a5553-168">On the **IdeaScale Configuration** section, click **Configure IdeaScale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a5553-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section**.</span><span class="sxs-lookup"><span data-stu-id="a5553-169">Copy the **Sign-Out URL, and SAML Entity ID** from the **Quick Reference section**.</span></span>

    ![Configure Single Sign-On](./media/ideascale-tutorial/tutorial_ideascale_configure.png) 

1. <span data-ttu-id="a5553-171">In a different web browser window, log in to your IdeaScale company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a5553-171">In a different web browser window, log in to your IdeaScale company site as an administrator.</span></span>

1. <span data-ttu-id="a5553-172">Go to **Community Settings**.</span><span class="sxs-lookup"><span data-stu-id="a5553-172">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="a5553-173">![Community Settings](./media/ideascale-tutorial/ic790847.png "Community Settings")</span><span class="sxs-lookup"><span data-stu-id="a5553-173">![Community Settings](./media/ideascale-tutorial/ic790847.png "Community Settings")</span></span>

1. <span data-ttu-id="a5553-174">Go to **Security \> Single Signon Settings**.</span><span class="sxs-lookup"><span data-stu-id="a5553-174">Go to **Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="a5553-175">![Single Signon Settings](./media/ideascale-tutorial/ic790848.png "Single Signon Settings")</span><span class="sxs-lookup"><span data-stu-id="a5553-175">![Single Signon Settings](./media/ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

1. <span data-ttu-id="a5553-176">As **Single-Signon Type**, select **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="a5553-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="a5553-177">![Single Signon Type](./media/ideascale-tutorial/ic790849.png "Single Signon Type")</span><span class="sxs-lookup"><span data-stu-id="a5553-177">![Single Signon Type](./media/ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

1. <span data-ttu-id="a5553-178">On the **Single Signon Settings** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a5553-178">On the **Single Signon Settings** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="a5553-179">![Single Signon Settings](./media/ideascale-tutorial/ic790850.png "Single Signon Settings")</span><span class="sxs-lookup"><span data-stu-id="a5553-179">![Single Signon Settings](./media/ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="a5553-180">a.</span><span class="sxs-lookup"><span data-stu-id="a5553-180">a.</span></span> <span data-ttu-id="a5553-181">In **SAML IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a5553-181">In **SAML IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a5553-182">b.</span><span class="sxs-lookup"><span data-stu-id="a5553-182">b.</span></span> <span data-ttu-id="a5553-183">Copy the content of your downloaded metadata file from Azure portal, and paste it into the **SAML IdP Metadata** textbox.</span><span class="sxs-lookup"><span data-stu-id="a5553-183">Copy the content of your downloaded metadata file from Azure portal, and paste it into the **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="a5553-184">c.</span><span class="sxs-lookup"><span data-stu-id="a5553-184">c.</span></span> <span data-ttu-id="a5553-185">In **Logout Success URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a5553-185">In **Logout Success URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a5553-186">d.</span><span class="sxs-lookup"><span data-stu-id="a5553-186">d.</span></span> <span data-ttu-id="a5553-187">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="a5553-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="a5553-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="a5553-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a5553-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="a5553-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a5553-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a5553-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a5553-191">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a5553-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="a5553-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a5553-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="a5553-194">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5553-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a5553-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="a5553-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/ideascale-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="a5553-197">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="a5553-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/ideascale-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="a5553-199">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="a5553-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/ideascale-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="a5553-201">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a5553-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a5553-203">a.</span><span class="sxs-lookup"><span data-stu-id="a5553-203">a.</span></span> <span data-ttu-id="a5553-204">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a5553-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a5553-205">b.</span><span class="sxs-lookup"><span data-stu-id="a5553-205">b.</span></span> <span data-ttu-id="a5553-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a5553-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a5553-207">c.</span><span class="sxs-lookup"><span data-stu-id="a5553-207">c.</span></span> <span data-ttu-id="a5553-208">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="a5553-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a5553-209">d.</span><span class="sxs-lookup"><span data-stu-id="a5553-209">d.</span></span> <span data-ttu-id="a5553-210">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a5553-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="a5553-211">Creating an IdeaScale test user</span><span class="sxs-lookup"><span data-stu-id="a5553-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="a5553-212">To enable Azure AD users to log into IdeaScale, they must be provisioned in to IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="a5553-212">To enable Azure AD users to log into IdeaScale, they must be provisioned in to IdeaScale.</span></span> <span data-ttu-id="a5553-213">In the case of IdeaScale, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="a5553-213">In the case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="a5553-214">**To configure user provisioning, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5553-214">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="a5553-215">Log in to your **IdeaScale** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="a5553-215">Log in to your **IdeaScale** company site as administrator.</span></span>

1. <span data-ttu-id="a5553-216">Go to **Community Settings**.</span><span class="sxs-lookup"><span data-stu-id="a5553-216">Go to **Community Settings**.</span></span>
   
    <span data-ttu-id="a5553-217">![Community Settings](./media/ideascale-tutorial/ic790847.png "Community Settings")</span><span class="sxs-lookup"><span data-stu-id="a5553-217">![Community Settings](./media/ideascale-tutorial/ic790847.png "Community Settings")</span></span>

1. <span data-ttu-id="a5553-218">Go to **Basic Settings \> Member Management**.</span><span class="sxs-lookup"><span data-stu-id="a5553-218">Go to **Basic Settings \> Member Management**.</span></span>

1. <span data-ttu-id="a5553-219">Click **Add Member**.</span><span class="sxs-lookup"><span data-stu-id="a5553-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="a5553-220">![Member Management](./media/ideascale-tutorial/ic790852.png "Member Management")</span><span class="sxs-lookup"><span data-stu-id="a5553-220">![Member Management](./media/ideascale-tutorial/ic790852.png "Member Management")</span></span>

1. <span data-ttu-id="a5553-221">In the Add New Member section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="a5553-221">In the Add New Member section, perform the following steps:</span></span>
   
    <span data-ttu-id="a5553-222">![Add New Member](./media/ideascale-tutorial/ic790853.png "Add New Member")</span><span class="sxs-lookup"><span data-stu-id="a5553-222">![Add New Member](./media/ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="a5553-223">a.</span><span class="sxs-lookup"><span data-stu-id="a5553-223">a.</span></span> <span data-ttu-id="a5553-224">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="a5553-224">In the **Email Addresses** textbox, type the email address of a valid AAD account you want to provision.</span></span>
   
    <span data-ttu-id="a5553-225">b.</span><span class="sxs-lookup"><span data-stu-id="a5553-225">b.</span></span> <span data-ttu-id="a5553-226">Click **Save Changes**.</span><span class="sxs-lookup"><span data-stu-id="a5553-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="a5553-227">The Azure Active Directory account holder gets an email with a link to confirm the account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="a5553-227">The Azure Active Directory account holder gets an email with a link to confirm the account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="a5553-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="a5553-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a5553-229">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="a5553-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a5553-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="a5553-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to IdeaScale.</span></span>

![Assign User][200] 

<span data-ttu-id="a5553-232">**To assign Britta Simon to IdeaScale, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="a5553-232">**To assign Britta Simon to IdeaScale, perform the following steps:**</span></span>

1. <span data-ttu-id="a5553-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="a5553-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="a5553-235">In the applications list, select **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="a5553-235">In the applications list, select **IdeaScale**.</span></span>

    ![Configure Single Sign-On](./media/ideascale-tutorial/tutorial_ideascale_app.png) 

1. <span data-ttu-id="a5553-237">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="a5553-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="a5553-239">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="a5553-239">Click **Add** button.</span></span> <span data-ttu-id="a5553-240">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a5553-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="a5553-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="a5553-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="a5553-243">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="a5553-243">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="a5553-244">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="a5553-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a5553-245">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="a5553-245">Testing single sign-on</span></span>


<span data-ttu-id="a5553-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a5553-246">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a5553-247">When you click the IdeaScale tile in the Access Panel, you should get automatically signed-on to your IdeaScale application.</span><span class="sxs-lookup"><span data-stu-id="a5553-247">When you click the IdeaScale tile in the Access Panel, you should get automatically signed-on to your IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a5553-248">Additional resources</span><span class="sxs-lookup"><span data-stu-id="a5553-248">Additional resources</span></span>

* [<span data-ttu-id="a5553-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5553-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="a5553-250">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a5553-250">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/ideascale-tutorial/tutorial_general_01.png
[2]: ./media/ideascale-tutorial/tutorial_general_02.png
[3]: ./media/ideascale-tutorial/tutorial_general_03.png
[4]: ./media/ideascale-tutorial/tutorial_general_04.png

[100]: ./media/ideascale-tutorial/tutorial_general_100.png

[200]: ./media/ideascale-tutorial/tutorial_general_200.png
[201]: ./media/ideascale-tutorial/tutorial_general_201.png
[202]: ./media/ideascale-tutorial/tutorial_general_202.png
[203]: ./media/ideascale-tutorial/tutorial_general_203.png

