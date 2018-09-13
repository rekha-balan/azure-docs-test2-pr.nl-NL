---
title: 'Tutorial: Azure Active Directory integration with ThirdLight | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ThirdLight.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 3ab87614e6c435abc5751b1da98f9ff3fb6cedb1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856750"
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="021c6-103">Tutorial: Azure Active Directory integration with ThirdLight</span><span class="sxs-lookup"><span data-stu-id="021c6-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="021c6-104">In this tutorial, you learn how to integrate ThirdLight with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="021c6-104">In this tutorial, you learn how to integrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="021c6-105">Integrating ThirdLight with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="021c6-105">Integrating ThirdLight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="021c6-106">You can control in Azure AD who has access to ThirdLight</span><span class="sxs-lookup"><span data-stu-id="021c6-106">You can control in Azure AD who has access to ThirdLight</span></span>
- <span data-ttu-id="021c6-107">You can enable your users to automatically get signed-on to ThirdLight (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="021c6-107">You can enable your users to automatically get signed-on to ThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="021c6-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="021c6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="021c6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="021c6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="021c6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="021c6-110">Prerequisites</span></span>

<span data-ttu-id="021c6-111">To configure Azure AD integration with ThirdLight, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="021c6-111">To configure Azure AD integration with ThirdLight, you need the following items:</span></span>

- <span data-ttu-id="021c6-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="021c6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="021c6-113">A ThirdLight single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="021c6-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="021c6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="021c6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="021c6-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="021c6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="021c6-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="021c6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="021c6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="021c6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="021c6-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="021c6-118">Scenario description</span></span>
<span data-ttu-id="021c6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="021c6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="021c6-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="021c6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="021c6-121">Adding ThirdLight from the gallery</span><span class="sxs-lookup"><span data-stu-id="021c6-121">Adding ThirdLight from the gallery</span></span>
1. <span data-ttu-id="021c6-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="021c6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-the-gallery"></a><span data-ttu-id="021c6-123">Adding ThirdLight from the gallery</span><span class="sxs-lookup"><span data-stu-id="021c6-123">Adding ThirdLight from the gallery</span></span>
<span data-ttu-id="021c6-124">To configure the integration of ThirdLight into Azure AD, you need to add ThirdLight from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="021c6-124">To configure the integration of ThirdLight into Azure AD, you need to add ThirdLight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="021c6-125">**To add ThirdLight from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="021c6-125">**To add ThirdLight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="021c6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="021c6-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="021c6-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="021c6-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="021c6-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="021c6-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="021c6-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="021c6-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="021c6-133">In the search box, type **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="021c6-133">In the search box, type **ThirdLight**.</span></span>

    ![Creating an Azure AD test user](./media/thirdlight-tutorial/tutorial_thirdlight_search.png)

1. <span data-ttu-id="021c6-135">In the results panel, select **ThirdLight**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="021c6-135">In the results panel, select **ThirdLight**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="021c6-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="021c6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="021c6-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="021c6-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="021c6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThirdLight is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="021c6-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThirdLight is to a user in Azure AD.</span></span> <span data-ttu-id="021c6-140">In other words, a link relationship between an Azure AD user and the related user in ThirdLight needs to be established.</span><span class="sxs-lookup"><span data-stu-id="021c6-140">In other words, a link relationship between an Azure AD user and the related user in ThirdLight needs to be established.</span></span>

<span data-ttu-id="021c6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="021c6-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ThirdLight.</span></span>

<span data-ttu-id="021c6-142">To configure and test Azure AD single sign-on with ThirdLight, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="021c6-142">To configure and test Azure AD single sign-on with ThirdLight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="021c6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="021c6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="021c6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="021c6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="021c6-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - to have a counterpart of Britta Simon in ThirdLight that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="021c6-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - to have a counterpart of Britta Simon in ThirdLight that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="021c6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="021c6-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="021c6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="021c6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="021c6-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="021c6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="021c6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThirdLight application.</span><span class="sxs-lookup"><span data-stu-id="021c6-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="021c6-150">**To configure Azure AD single sign-on with ThirdLight, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="021c6-150">**To configure Azure AD single sign-on with ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="021c6-151">In the Azure portal, on the **ThirdLight** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="021c6-151">In the Azure portal, on the **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="021c6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="021c6-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

1. <span data-ttu-id="021c6-155">On the **ThirdLight Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="021c6-155">On the **ThirdLight Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="021c6-157">a.</span><span class="sxs-lookup"><span data-stu-id="021c6-157">a.</span></span> <span data-ttu-id="021c6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="021c6-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="021c6-159">b.</span><span class="sxs-lookup"><span data-stu-id="021c6-159">b.</span></span> <span data-ttu-id="021c6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="021c6-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="021c6-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="021c6-161">These values are not real.</span></span> <span data-ttu-id="021c6-162">Update these values with the actual Sign-On URL and Identiifer.</span><span class="sxs-lookup"><span data-stu-id="021c6-162">Update these values with the actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="021c6-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="021c6-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) to get these values.</span></span> 
 
1. <span data-ttu-id="021c6-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span><span class="sxs-lookup"><span data-stu-id="021c6-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Configure Single Sign-On](./media/thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

1. <span data-ttu-id="021c6-166">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="021c6-166">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/thirdlight-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="021c6-168">In a different web browser window, log in to your ThirdLight company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="021c6-168">In a different web browser window, log in to your ThirdLight company site as an administrator.</span></span>

1. <span data-ttu-id="021c6-169">Go to **Configuration \> System Administration**, and then click **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="021c6-169">Go to **Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="021c6-170">![System Administration](./media/thirdlight-tutorial/ic805843.png "System Administration")</span><span class="sxs-lookup"><span data-stu-id="021c6-170">![System Administration](./media/thirdlight-tutorial/ic805843.png "System Administration")</span></span>

1. <span data-ttu-id="021c6-171">In the SAML2 configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="021c6-171">In the SAML2 configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="021c6-172">![SAML Single Sign-On](./media/thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span><span class="sxs-lookup"><span data-stu-id="021c6-172">![SAML Single Sign-On](./media/thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="021c6-173">a.</span><span class="sxs-lookup"><span data-stu-id="021c6-173">a.</span></span> <span data-ttu-id="021c6-174">Select **Enable SAML2 Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="021c6-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="021c6-175">b.</span><span class="sxs-lookup"><span data-stu-id="021c6-175">b.</span></span> <span data-ttu-id="021c6-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span><span class="sxs-lookup"><span data-stu-id="021c6-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="021c6-177">c.</span><span class="sxs-lookup"><span data-stu-id="021c6-177">c.</span></span> <span data-ttu-id="021c6-178">Open the downloaded metadata file, copy the content, and then paste it into the **IdP Metadata XML** textbox.</span><span class="sxs-lookup"><span data-stu-id="021c6-178">Open the downloaded metadata file, copy the content, and then paste it into the **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="021c6-179">d.</span><span class="sxs-lookup"><span data-stu-id="021c6-179">d.</span></span> <span data-ttu-id="021c6-180">Click **Save SAML2 settings**.</span><span class="sxs-lookup"><span data-stu-id="021c6-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="021c6-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="021c6-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="021c6-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="021c6-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="021c6-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="021c6-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="021c6-184">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="021c6-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="021c6-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="021c6-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="021c6-187">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="021c6-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="021c6-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="021c6-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/thirdlight-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="021c6-190">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="021c6-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/thirdlight-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="021c6-192">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="021c6-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/thirdlight-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="021c6-194">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="021c6-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="021c6-196">a.</span><span class="sxs-lookup"><span data-stu-id="021c6-196">a.</span></span> <span data-ttu-id="021c6-197">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="021c6-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="021c6-198">b.</span><span class="sxs-lookup"><span data-stu-id="021c6-198">b.</span></span> <span data-ttu-id="021c6-199">In the **User name** textbox, type the **email address** of Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="021c6-199">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="021c6-200">c.</span><span class="sxs-lookup"><span data-stu-id="021c6-200">c.</span></span> <span data-ttu-id="021c6-201">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="021c6-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="021c6-202">d.</span><span class="sxs-lookup"><span data-stu-id="021c6-202">d.</span></span> <span data-ttu-id="021c6-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="021c6-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="021c6-204">Creating a ThirdLight test user</span><span class="sxs-lookup"><span data-stu-id="021c6-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="021c6-205">To enable Azure AD users to log in to ThirdLight, they must be provisioned into ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="021c6-205">To enable Azure AD users to log in to ThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="021c6-206">In the case of ThirdLight, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="021c6-206">In the case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="021c6-207">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="021c6-207">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="021c6-208">Log in to your **ThirdLight** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="021c6-208">Log in to your **ThirdLight** company site as an administrator.</span></span>

1. <span data-ttu-id="021c6-209">Go to **Users** tab.</span><span class="sxs-lookup"><span data-stu-id="021c6-209">Go to **Users** tab.</span></span>

1. <span data-ttu-id="021c6-210">Select **Users and Groups**.</span><span class="sxs-lookup"><span data-stu-id="021c6-210">Select **Users and Groups**.</span></span>

1. <span data-ttu-id="021c6-211">Click **Add new User** button.</span><span class="sxs-lookup"><span data-stu-id="021c6-211">Click **Add new User** button.</span></span>

1. <span data-ttu-id="021c6-212">Enter **the Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="021c6-212">Enter **the Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want to provision.</span></span>

1. <span data-ttu-id="021c6-213">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="021c6-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="021c6-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="021c6-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="021c6-215">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="021c6-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="021c6-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="021c6-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThirdLight.</span></span>

![Assign User][200] 

<span data-ttu-id="021c6-218">**To assign Britta Simon to ThirdLight, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="021c6-218">**To assign Britta Simon to ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="021c6-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="021c6-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="021c6-221">In the applications list, select **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="021c6-221">In the applications list, select **ThirdLight**.</span></span>

    ![Configure Single Sign-On](./media/thirdlight-tutorial/tutorial_thirdlight_app.png) 

1. <span data-ttu-id="021c6-223">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="021c6-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="021c6-225">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="021c6-225">Click **Add** button.</span></span> <span data-ttu-id="021c6-226">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="021c6-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="021c6-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="021c6-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="021c6-229">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="021c6-229">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="021c6-230">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="021c6-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="021c6-231">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="021c6-231">Testing single sign-on</span></span>

<span data-ttu-id="021c6-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="021c6-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="021c6-233">When you click the ThirdLight tile in the Access Panel, you should get automatically signed-on to your ThirdLight application.</span><span class="sxs-lookup"><span data-stu-id="021c6-233">When you click the ThirdLight tile in the Access Panel, you should get automatically signed-on to your ThirdLight application.</span></span>
<span data-ttu-id="021c6-234">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="021c6-234">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="021c6-235">Additional resources</span><span class="sxs-lookup"><span data-stu-id="021c6-235">Additional resources</span></span>

* [<span data-ttu-id="021c6-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="021c6-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="021c6-237">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="021c6-237">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/thirdlight-tutorial/tutorial_general_203.png

