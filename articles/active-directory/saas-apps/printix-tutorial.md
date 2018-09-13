---
title: 'Tutorial: Azure Active Directory integration with Printix | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Printix.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 4aea7320-b2d5-49e0-9b63-aeaff0f6fe66
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 5b4672ad65b152861ea521883cea781aba6abf17
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856269"
---
# <a name="tutorial-azure-active-directory-integration-with-printix"></a><span data-ttu-id="d49cb-103">Tutorial: Azure Active Directory integration with Printix</span><span class="sxs-lookup"><span data-stu-id="d49cb-103">Tutorial: Azure Active Directory integration with Printix</span></span>

<span data-ttu-id="d49cb-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d49cb-104">In this tutorial, you learn how to integrate Printix with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d49cb-105">Integrating Printix with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d49cb-105">Integrating Printix with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d49cb-106">You can control in Azure AD who has access to Printix</span><span class="sxs-lookup"><span data-stu-id="d49cb-106">You can control in Azure AD who has access to Printix</span></span>
- <span data-ttu-id="d49cb-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d49cb-107">You can enable your users to automatically get signed-on to Printix (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d49cb-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d49cb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d49cb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d49cb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d49cb-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d49cb-110">Prerequisites</span></span>

<span data-ttu-id="d49cb-111">To configure Azure AD integration with Printix, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d49cb-111">To configure Azure AD integration with Printix, you need the following items:</span></span>

- <span data-ttu-id="d49cb-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d49cb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d49cb-113">A Printix single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d49cb-113">A Printix single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d49cb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d49cb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d49cb-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d49cb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d49cb-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d49cb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d49cb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d49cb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d49cb-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d49cb-118">Scenario description</span></span>
<span data-ttu-id="d49cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d49cb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d49cb-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d49cb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d49cb-121">Adding Printix from the gallery</span><span class="sxs-lookup"><span data-stu-id="d49cb-121">Adding Printix from the gallery</span></span>
1. <span data-ttu-id="d49cb-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d49cb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-printix-from-the-gallery"></a><span data-ttu-id="d49cb-123">Adding Printix from the gallery</span><span class="sxs-lookup"><span data-stu-id="d49cb-123">Adding Printix from the gallery</span></span>
<span data-ttu-id="d49cb-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d49cb-124">To configure the integration of Printix into Azure AD, you need to add Printix from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d49cb-125">**To add Printix from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d49cb-125">**To add Printix from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d49cb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d49cb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="d49cb-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d49cb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d49cb-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d49cb-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="d49cb-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d49cb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="d49cb-133">In the search box, type **Printix**.</span><span class="sxs-lookup"><span data-stu-id="d49cb-133">In the search box, type **Printix**.</span></span>

    ![Creating an Azure AD test user](./media/printix-tutorial/tutorial_printix_search.png)

1. <span data-ttu-id="d49cb-135">In the results panel, select **Printix**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d49cb-135">In the results panel, select **Printix**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/printix-tutorial/tutorial_printix_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d49cb-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d49cb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d49cb-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d49cb-138">In this section, you configure and test Azure AD single sign-on with Printix based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d49cb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d49cb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Printix is to a user in Azure AD.</span></span> <span data-ttu-id="d49cb-140">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d49cb-140">In other words, a link relationship between an Azure AD user and the related user in Printix needs to be established.</span></span>

<span data-ttu-id="d49cb-141">In Printix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="d49cb-141">In Printix, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d49cb-142">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d49cb-142">To configure and test Azure AD single sign-on with Printix, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d49cb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d49cb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d49cb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d49cb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d49cb-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d49cb-145">**[Creating a Printix test user](#creating-a-printix-test-user)** - to have a counterpart of Britta Simon in Printix that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d49cb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d49cb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d49cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d49cb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d49cb-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d49cb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d49cb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Printix application.</span><span class="sxs-lookup"><span data-stu-id="d49cb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Printix application.</span></span>

<span data-ttu-id="d49cb-150">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d49cb-150">**To configure Azure AD single sign-on with Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="d49cb-151">In the Azure portal, on the **Printix** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d49cb-151">In the Azure portal, on the **Printix** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="d49cb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d49cb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/printix-tutorial/tutorial_printix_samlbase.png)

1. <span data-ttu-id="d49cb-155">On the **Printix Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d49cb-155">On the **Printix Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/printix-tutorial/tutorial_printix_url.png)

    <span data-ttu-id="d49cb-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.printix.net`</span><span class="sxs-lookup"><span data-stu-id="d49cb-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.printix.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d49cb-158">The value is not real.</span><span class="sxs-lookup"><span data-stu-id="d49cb-158">The value is not real.</span></span> <span data-ttu-id="d49cb-159">Update the value with the actual Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="d49cb-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="d49cb-160">Contact [Printix Client support team](mailto:support@printix.net) to get the value.</span><span class="sxs-lookup"><span data-stu-id="d49cb-160">Contact [Printix Client support team](mailto:support@printix.net) to get the value.</span></span> 
 
1. <span data-ttu-id="d49cb-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d49cb-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/printix-tutorial/tutorial_printix_certificate.png) 

1. <span data-ttu-id="d49cb-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d49cb-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/printix-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="d49cb-165">Sign-on to your Printix tenant as an administrator.</span><span class="sxs-lookup"><span data-stu-id="d49cb-165">Sign-on to your Printix tenant as an administrator.</span></span>

1. <span data-ttu-id="d49cb-166">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span><span class="sxs-lookup"><span data-stu-id="d49cb-166">In the menu on the top, click the icon at the upper right corner and select "**Authentication**".</span></span>
   
    ![Configure Single Sign-On](./media/printix-tutorial/tutorial_printix_06.png)

1. <span data-ttu-id="d49cb-168">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span><span class="sxs-lookup"><span data-stu-id="d49cb-168">On the **Setup** tab, select **Enable Azure/Office 365 authentication**</span></span>
   
    ![Configure Single Sign-On](./media/printix-tutorial/tutorial_printix_07.png)

1. <span data-ttu-id="d49cb-170">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span><span class="sxs-lookup"><span data-stu-id="d49cb-170">On the **Azure** tab, input federation metadata URL to the textbox of "**Federation metadata document**".</span></span> 

    <span data-ttu-id="d49cb-171">Attach the metadata xml file which you downloaded from Azure AD to [Printix support team](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="d49cb-171">Attach the metadata xml file which you downloaded from Azure AD to [Printix support team](mailto:support@printix.net).</span></span> <span data-ttu-id="d49cb-172">Then they upload the xml file and provide a federation metadata URL.</span><span class="sxs-lookup"><span data-stu-id="d49cb-172">Then they upload the xml file and provide a federation metadata URL.</span></span>
   
    ![Configure Single Sign-On](./media/printix-tutorial/tutorial_printix_08.png)
   
1. <span data-ttu-id="d49cb-174">Click the "**Test**" button and click "**OK**" button if the test was successful.</span><span class="sxs-lookup"><span data-stu-id="d49cb-174">Click the "**Test**" button and click "**OK**" button if the test was successful.</span></span>
   
     <span data-ttu-id="d49cb-175">Azure active directory page will show after clicking the **test** button.</span><span class="sxs-lookup"><span data-stu-id="d49cb-175">Azure active directory page will show after clicking the **test** button.</span></span> <span data-ttu-id="d49cb-176">"The test was successful" here means after entering the credentials of your Azure test account it will pop up a message "Settings tested OK".Then click the **OK** button.</span><span class="sxs-lookup"><span data-stu-id="d49cb-176">"The test was successful" here means after entering the credentials of your Azure test account it will pop up a message "Settings tested OK".Then click the **OK** button.</span></span>
   
    ![Configure Single Sign-On](./media/printix-tutorial/tutorial_printix_09.png)

1. <span data-ttu-id="d49cb-178">Click the **Save** button on "**Authentication**" page.</span><span class="sxs-lookup"><span data-stu-id="d49cb-178">Click the **Save** button on "**Authentication**" page.</span></span>


> [!TIP]
> <span data-ttu-id="d49cb-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="d49cb-179">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d49cb-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d49cb-180">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d49cb-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d49cb-181">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d49cb-182">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d49cb-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="d49cb-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d49cb-183">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="d49cb-185">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d49cb-185">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d49cb-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d49cb-186">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/printix-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="d49cb-188">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d49cb-188">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/printix-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="d49cb-190">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="d49cb-190">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/printix-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="d49cb-192">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d49cb-192">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/printix-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d49cb-194">a.</span><span class="sxs-lookup"><span data-stu-id="d49cb-194">a.</span></span> <span data-ttu-id="d49cb-195">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d49cb-195">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d49cb-196">b.</span><span class="sxs-lookup"><span data-stu-id="d49cb-196">b.</span></span> <span data-ttu-id="d49cb-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d49cb-197">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d49cb-198">c.</span><span class="sxs-lookup"><span data-stu-id="d49cb-198">c.</span></span> <span data-ttu-id="d49cb-199">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="d49cb-199">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d49cb-200">d.</span><span class="sxs-lookup"><span data-stu-id="d49cb-200">d.</span></span> <span data-ttu-id="d49cb-201">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d49cb-201">Click **Create**.</span></span>
 
### <a name="creating-a-printix-test-user"></a><span data-ttu-id="d49cb-202">Creating a Printix test user</span><span class="sxs-lookup"><span data-stu-id="d49cb-202">Creating a Printix test user</span></span>

<span data-ttu-id="d49cb-203">The objective of this section is to create a user called Britta Simon in Printix.</span><span class="sxs-lookup"><span data-stu-id="d49cb-203">The objective of this section is to create a user called Britta Simon in Printix.</span></span> <span data-ttu-id="d49cb-204">Printix supports just-in-time provisioning, which is by default enabled.</span><span class="sxs-lookup"><span data-stu-id="d49cb-204">Printix supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="d49cb-205">There is no action item for you in this section.</span><span class="sxs-lookup"><span data-stu-id="d49cb-205">There is no action item for you in this section.</span></span> <span data-ttu-id="d49cb-206">A new user is created during an attempt to access Printix if it doesn't exist yet.</span><span class="sxs-lookup"><span data-stu-id="d49cb-206">A new user is created during an attempt to access Printix if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="d49cb-207">If you need to create a user manually, you need to contact the [Printix support team](mailto:support@printix.net).</span><span class="sxs-lookup"><span data-stu-id="d49cb-207">If you need to create a user manually, you need to contact the [Printix support team](mailto:support@printix.net).</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d49cb-208">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d49cb-208">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d49cb-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Printix.</span><span class="sxs-lookup"><span data-stu-id="d49cb-209">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Printix.</span></span>

![Assign User][200] 

<span data-ttu-id="d49cb-211">**To assign Britta Simon to Printix, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d49cb-211">**To assign Britta Simon to Printix, perform the following steps:**</span></span>

1. <span data-ttu-id="d49cb-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d49cb-212">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d49cb-214">In the applications list, select **Printix**.</span><span class="sxs-lookup"><span data-stu-id="d49cb-214">In the applications list, select **Printix**.</span></span>

    ![Configure Single Sign-On](./media/printix-tutorial/tutorial_printix_app.png) 

1. <span data-ttu-id="d49cb-216">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d49cb-216">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="d49cb-218">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d49cb-218">Click **Add** button.</span></span> <span data-ttu-id="d49cb-219">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d49cb-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="d49cb-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d49cb-221">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d49cb-222">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d49cb-222">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d49cb-223">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d49cb-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d49cb-224">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="d49cb-224">Testing single sign-on</span></span>

<span data-ttu-id="d49cb-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d49cb-225">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d49cb-226">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span><span class="sxs-lookup"><span data-stu-id="d49cb-226">When you click the Printix tile in the Access Panel, you should get automatically signed-on to your Printix application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d49cb-227">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d49cb-227">Additional resources</span></span>

* [<span data-ttu-id="d49cb-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d49cb-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d49cb-229">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d49cb-229">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/printix-tutorial/tutorial_general_01.png
[2]: ./media/printix-tutorial/tutorial_general_02.png
[3]: ./media/printix-tutorial/tutorial_general_03.png
[4]: ./media/printix-tutorial/tutorial_general_04.png

[100]: ./media/printix-tutorial/tutorial_general_100.png

[200]: ./media/printix-tutorial/tutorial_general_200.png
[201]: ./media/printix-tutorial/tutorial_general_201.png
[202]: ./media/printix-tutorial/tutorial_general_202.png
[203]: ./media/printix-tutorial/tutorial_general_203.png

