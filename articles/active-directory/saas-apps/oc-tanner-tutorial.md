---
title: 'Tutorial: Azure Active Directory integration with O.C. Tanner - AppreciateHub | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and O.C. Tanner - AppreciateHub.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: jeedes
ms.openlocfilehash: 2a3c6641c3fd9402ede2176e3c5c3f3ec15ed9de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856839"
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="d79ce-105">Tutorial: Azure Active Directory integration with O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="d79ce-106">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="d79ce-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="d79ce-107">In this tutorial, you learn how to integrate O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-107">In this tutorial, you learn how to integrate O.C.</span></span> <span data-ttu-id="d79ce-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d79ce-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d79ce-109">Integrating O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-109">Integrating O.C.</span></span> <span data-ttu-id="d79ce-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="d79ce-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d79ce-111">You can control in Azure AD who has access to O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-111">You can control in Azure AD who has access to O.C.</span></span> <span data-ttu-id="d79ce-112">Tanner - AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="d79ce-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="d79ce-113">You can enable your users to automatically get signed-on to O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-113">You can enable your users to automatically get signed-on to O.C.</span></span> <span data-ttu-id="d79ce-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="d79ce-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d79ce-115">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d79ce-115">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d79ce-116">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="d79ce-116">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d79ce-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d79ce-117">Prerequisites</span></span>

<span data-ttu-id="d79ce-118">To configure Azure AD integration with O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-118">To configure Azure AD integration with O.C.</span></span> <span data-ttu-id="d79ce-119">Tanner - AppreciateHub, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="d79ce-119">Tanner - AppreciateHub, you need the following items:</span></span>

- <span data-ttu-id="d79ce-120">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="d79ce-120">An Azure AD subscription</span></span>
- <span data-ttu-id="d79ce-121">A O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-121">A O.C.</span></span> <span data-ttu-id="d79ce-122">Tanner - AppreciateHub single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="d79ce-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d79ce-123">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="d79ce-123">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d79ce-124">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="d79ce-124">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d79ce-125">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="d79ce-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d79ce-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d79ce-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d79ce-127">Scenario description</span><span class="sxs-lookup"><span data-stu-id="d79ce-127">Scenario description</span></span>
<span data-ttu-id="d79ce-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="d79ce-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d79ce-129">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="d79ce-129">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d79ce-130">Adding O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-130">Adding O.C.</span></span> <span data-ttu-id="d79ce-131">Tanner - AppreciateHub from the gallery</span><span class="sxs-lookup"><span data-stu-id="d79ce-131">Tanner - AppreciateHub from the gallery</span></span>
1. <span data-ttu-id="d79ce-132">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d79ce-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a><span data-ttu-id="d79ce-133">Adding O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-133">Adding O.C.</span></span> <span data-ttu-id="d79ce-134">Tanner - AppreciateHub from the gallery</span><span class="sxs-lookup"><span data-stu-id="d79ce-134">Tanner - AppreciateHub from the gallery</span></span>
<span data-ttu-id="d79ce-135">To configure the integration of O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-135">To configure the integration of O.C.</span></span> <span data-ttu-id="d79ce-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span></span> <span data-ttu-id="d79ce-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d79ce-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d79ce-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d79ce-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d79ce-139">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d79ce-139">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="d79ce-141">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="d79ce-141">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d79ce-142">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d79ce-142">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="d79ce-144">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="d79ce-144">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="d79ce-146">In the search box, type **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="d79ce-146">In the search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Creating an Azure AD test user](./media/oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

1. <span data-ttu-id="d79ce-148">In the results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="d79ce-148">In the results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d79ce-150">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d79ce-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d79ce-151">In this section, you configure and test Azure AD single sign-on with O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="d79ce-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="d79ce-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d79ce-153">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-153">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span></span> <span data-ttu-id="d79ce-154">Tanner - AppreciateHub is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d79ce-154">Tanner - AppreciateHub is to a user in Azure AD.</span></span> <span data-ttu-id="d79ce-155">In other words, a link relationship between an Azure AD user and the related user in O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-155">In other words, a link relationship between an Azure AD user and the related user in O.C.</span></span> <span data-ttu-id="d79ce-156">Tanner - AppreciateHub needs to be established.</span><span class="sxs-lookup"><span data-stu-id="d79ce-156">Tanner - AppreciateHub needs to be established.</span></span>

<span data-ttu-id="d79ce-157">In O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-157">In O.C.</span></span> <span data-ttu-id="d79ce-158">Tanner - AppreciateHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="d79ce-158">Tanner - AppreciateHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d79ce-159">To configure and test Azure AD single sign-on with O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-159">To configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="d79ce-160">Tanner - AppreciateHub, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="d79ce-160">Tanner - AppreciateHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d79ce-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="d79ce-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="d79ce-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d79ce-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="d79ce-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - to have a counterpart of Britta Simon in O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - to have a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="d79ce-164">Tanner - AppreciateHub that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="d79ce-164">Tanner - AppreciateHub that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="d79ce-165">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d79ce-165">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="d79ce-166">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="d79ce-166">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d79ce-167">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="d79ce-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d79ce-168">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-168">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="d79ce-169">Tanner - AppreciateHub application.</span><span class="sxs-lookup"><span data-stu-id="d79ce-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="d79ce-170">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d79ce-170">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="d79ce-171">In the Azure portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="d79ce-171">In the Azure portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="d79ce-173">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="d79ce-173">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

1. <span data-ttu-id="d79ce-175">On the **O.C. Tanner - AppreciateHub Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d79ce-175">On the **O.C. Tanner - AppreciateHub Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="d79ce-177">a.</span><span class="sxs-lookup"><span data-stu-id="d79ce-177">a.</span></span> <span data-ttu-id="d79ce-178">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.octanner.net/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="d79ce-178">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.octanner.net/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d79ce-179">This value is not real.</span><span class="sxs-lookup"><span data-stu-id="d79ce-179">This value is not real.</span></span> <span data-ttu-id="d79ce-180">Update this value with the actual Reply URL.</span><span class="sxs-lookup"><span data-stu-id="d79ce-180">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="d79ce-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to get this value.</span><span class="sxs-lookup"><span data-stu-id="d79ce-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to get this value.</span></span>

    <span data-ttu-id="d79ce-182">b.</span><span class="sxs-lookup"><span data-stu-id="d79ce-182">b.</span></span> <span data-ttu-id="d79ce-183">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="d79ce-183">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="d79ce-184">c.</span><span class="sxs-lookup"><span data-stu-id="d79ce-184">c.</span></span> <span data-ttu-id="d79ce-185">Locate the **md:AssertionConsumerService** node.</span><span class="sxs-lookup"><span data-stu-id="d79ce-185">Locate the **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="d79ce-186">d.</span><span class="sxs-lookup"><span data-stu-id="d79ce-186">d.</span></span> <span data-ttu-id="d79ce-187">Copy the value of the **Location** attribute.</span><span class="sxs-lookup"><span data-stu-id="d79ce-187">Copy the value of the **Location** attribute.</span></span> 
   
    ![Configure App Settings][12]
   
    <span data-ttu-id="d79ce-189">e.</span><span class="sxs-lookup"><span data-stu-id="d79ce-189">e.</span></span> <span data-ttu-id="d79ce-190">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="d79ce-190">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span></span>

1. <span data-ttu-id="d79ce-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="d79ce-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

1. <span data-ttu-id="d79ce-193">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="d79ce-193">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/oc-tanner-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="d79ce-195">To configure single sign-on on **O.C. Tanner - AppreciateHub** side, you need to send the downloaded **Metadata XML** to [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="d79ce-195">To configure single sign-on on **O.C. Tanner - AppreciateHub** side, you need to send the downloaded **Metadata XML** to [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="d79ce-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="d79ce-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d79ce-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="d79ce-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d79ce-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d79ce-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d79ce-199">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d79ce-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="d79ce-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d79ce-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="d79ce-202">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d79ce-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d79ce-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="d79ce-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/oc-tanner-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="d79ce-205">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="d79ce-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/oc-tanner-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="d79ce-207">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="d79ce-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/oc-tanner-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="d79ce-209">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="d79ce-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d79ce-211">a.</span><span class="sxs-lookup"><span data-stu-id="d79ce-211">a.</span></span> <span data-ttu-id="d79ce-212">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d79ce-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d79ce-213">b.</span><span class="sxs-lookup"><span data-stu-id="d79ce-213">b.</span></span> <span data-ttu-id="d79ce-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d79ce-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d79ce-215">c.</span><span class="sxs-lookup"><span data-stu-id="d79ce-215">c.</span></span> <span data-ttu-id="d79ce-216">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="d79ce-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d79ce-217">d.</span><span class="sxs-lookup"><span data-stu-id="d79ce-217">d.</span></span> <span data-ttu-id="d79ce-218">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d79ce-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="d79ce-219">Creating a O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-219">Creating a O.C.</span></span> <span data-ttu-id="d79ce-220">Tanner - AppreciateHub test user</span><span class="sxs-lookup"><span data-stu-id="d79ce-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="d79ce-221">The objective of this section is to create a user called Britta Simon in O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-221">The objective of this section is to create a user called Britta Simon in O.C.</span></span> <span data-ttu-id="d79ce-222">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="d79ce-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="d79ce-223">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d79ce-223">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

<span data-ttu-id="d79ce-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d79ce-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d79ce-225">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="d79ce-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d79ce-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to O.C.</span></span> <span data-ttu-id="d79ce-227">Tanner - AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="d79ce-227">Tanner - AppreciateHub.</span></span>

![Assign User][200] 

<span data-ttu-id="d79ce-229">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="d79ce-229">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="d79ce-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="d79ce-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="d79ce-232">In the applications list, select **O.C. Tanner - AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="d79ce-232">In the applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Configure Single Sign-On](./media/oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

1. <span data-ttu-id="d79ce-234">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="d79ce-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="d79ce-236">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="d79ce-236">Click **Add** button.</span></span> <span data-ttu-id="d79ce-237">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d79ce-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="d79ce-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="d79ce-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="d79ce-240">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="d79ce-240">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="d79ce-241">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="d79ce-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d79ce-242">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="d79ce-242">Testing single sign-on</span></span>

<span data-ttu-id="d79ce-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="d79ce-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="d79ce-244">When you click the O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-244">When you click the O.C.</span></span> <span data-ttu-id="d79ce-245">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span><span class="sxs-lookup"><span data-stu-id="d79ce-245">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span></span> <span data-ttu-id="d79ce-246">Tanner - AppreciateHub application.</span><span class="sxs-lookup"><span data-stu-id="d79ce-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d79ce-247">Additional resources</span><span class="sxs-lookup"><span data-stu-id="d79ce-247">Additional resources</span></span>

* [<span data-ttu-id="d79ce-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d79ce-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="d79ce-249">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d79ce-249">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/oc-tanner-tutorial/tutorial_general_203.png

