---
title: 'Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Splunk Enterprise and Splunk Cloud.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: b1eb8f198b0d9e25a6514e19794c9b1d54a4cd3e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857599"
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="e181f-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="e181f-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="e181f-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e181f-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e181f-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="e181f-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e181f-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="e181f-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="e181f-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="e181f-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e181f-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e181f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e181f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="e181f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e181f-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e181f-110">Prerequisites</span></span>

<span data-ttu-id="e181f-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="e181f-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="e181f-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="e181f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e181f-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="e181f-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e181f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="e181f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e181f-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="e181f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e181f-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="e181f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e181f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e181f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e181f-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="e181f-118">Scenario description</span></span>
<span data-ttu-id="e181f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="e181f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e181f-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="e181f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e181f-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="e181f-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
1. <span data-ttu-id="e181f-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e181f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="e181f-123">Adding Splunk Enterprise and Splunk Cloud from the gallery</span><span class="sxs-lookup"><span data-stu-id="e181f-123">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="e181f-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="e181f-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e181f-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e181f-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e181f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e181f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="e181f-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="e181f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e181f-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e181f-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="e181f-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="e181f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="e181f-133">In the search box, type **Splunk Enterprise and Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="e181f-133">In the search box, type **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Creating an Azure AD test user](./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_search.png)

1. <span data-ttu-id="e181f-135">In the results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="e181f-135">In the results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e181f-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e181f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e181f-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="e181f-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e181f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e181f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="e181f-140">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span><span class="sxs-lookup"><span data-stu-id="e181f-140">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="e181f-141">In Splunk Enterprise and Splunk Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="e181f-141">In Splunk Enterprise and Splunk Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e181f-142">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="e181f-142">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e181f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="e181f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="e181f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e181f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="e181f-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="e181f-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="e181f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e181f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="e181f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="e181f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e181f-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="e181f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e181f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span><span class="sxs-lookup"><span data-stu-id="e181f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span></span>

<span data-ttu-id="e181f-150">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e181f-150">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="e181f-151">In the Azure portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="e181f-151">In the Azure portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="e181f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="e181f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_samlbase.png)

1. <span data-ttu-id="e181f-155">On the **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span><span class="sxs-lookup"><span data-stu-id="e181f-155">On the **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Configure Single Sign-On](./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_url.png)

    <span data-ttu-id="e181f-157">a.</span><span class="sxs-lookup"><span data-stu-id="e181f-157">a.</span></span> <span data-ttu-id="e181f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="e181f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
    
    <span data-ttu-id="e181f-159">b.</span><span class="sxs-lookup"><span data-stu-id="e181f-159">b.</span></span> <span data-ttu-id="e181f-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span><span class="sxs-lookup"><span data-stu-id="e181f-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>

    <span data-ttu-id="e181f-161">c.</span><span class="sxs-lookup"><span data-stu-id="e181f-161">c.</span></span> <span data-ttu-id="e181f-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="e181f-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<splunkserver>/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e181f-163">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="e181f-163">These values are not real.</span></span> <span data-ttu-id="e181f-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="e181f-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="e181f-165">Here we suggest you to use the unique value of string in the Identifier.</span><span class="sxs-lookup"><span data-stu-id="e181f-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="e181f-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="e181f-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) to get these values.</span></span> 

1. <span data-ttu-id="e181f-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="e181f-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_certificate.png) 

1. <span data-ttu-id="e181f-169">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="e181f-169">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="e181f-171">To configure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need to send the downloaded **Metadata XML** to [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="e181f-171">To configure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need to send the downloaded **Metadata XML** to [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span></span>

> [!TIP]
> <span data-ttu-id="e181f-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="e181f-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e181f-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="e181f-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e181f-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e181f-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e181f-175">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e181f-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="e181f-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e181f-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="e181f-178">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e181f-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e181f-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="e181f-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/splunkenterpriseandsplunkcloud-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="e181f-181">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="e181f-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/splunkenterpriseandsplunkcloud-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="e181f-183">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="e181f-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/splunkenterpriseandsplunkcloud-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="e181f-185">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="e181f-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/splunkenterpriseandsplunkcloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e181f-187">a.</span><span class="sxs-lookup"><span data-stu-id="e181f-187">a.</span></span> <span data-ttu-id="e181f-188">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e181f-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e181f-189">b.</span><span class="sxs-lookup"><span data-stu-id="e181f-189">b.</span></span> <span data-ttu-id="e181f-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e181f-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e181f-191">c.</span><span class="sxs-lookup"><span data-stu-id="e181f-191">c.</span></span> <span data-ttu-id="e181f-192">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="e181f-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e181f-193">d.</span><span class="sxs-lookup"><span data-stu-id="e181f-193">d.</span></span> <span data-ttu-id="e181f-194">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e181f-194">Click **Create**.</span></span>
 
### <a name="creating-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="e181f-195">Creating a Splunk Enterprise and Splunk Cloud test user</span><span class="sxs-lookup"><span data-stu-id="e181f-195">Creating a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="e181f-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="e181f-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="e181f-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) to add the users in the Splunk Enterprise and Splunk Cloud platform.</span><span class="sxs-lookup"><span data-stu-id="e181f-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e181f-198">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="e181f-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e181f-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Splunk Enterprise and Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="e181f-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Splunk Enterprise and Splunk Cloud.</span></span>

![Assign User][200] 

<span data-ttu-id="e181f-201">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="e181f-201">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="e181f-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="e181f-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="e181f-204">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="e181f-204">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Configure Single Sign-On](./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_app.png) 

1. <span data-ttu-id="e181f-206">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="e181f-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="e181f-208">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e181f-208">Click **Add** button.</span></span> <span data-ttu-id="e181f-209">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e181f-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="e181f-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="e181f-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="e181f-212">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="e181f-212">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="e181f-213">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="e181f-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e181f-214">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="e181f-214">Testing single sign-on</span></span>

<span data-ttu-id="e181f-215">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="e181f-215">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="e181f-216">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span><span class="sxs-lookup"><span data-stu-id="e181f-216">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e181f-217">Additional resources</span><span class="sxs-lookup"><span data-stu-id="e181f-217">Additional resources</span></span>

* [<span data-ttu-id="e181f-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e181f-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="e181f-219">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e181f-219">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)


<!--Image references-->

[1]: ./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_general_01.png
[2]: ./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_general_02.png
[3]: ./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_general_03.png
[4]: ./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_general_04.png

[100]: ./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_general_100.png

[200]: ./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_general_200.png
[201]: ./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_general_201.png
[202]: ./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_general_202.png
[203]: ./media/splunkenterpriseandsplunkcloud-tutorial/tutorial_general_203.png

