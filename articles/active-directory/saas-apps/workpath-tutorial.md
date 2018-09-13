---
title: 'Tutorial: Azure Active Directory integration with Workpath | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Workpath.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 320b0daf-14be-4813-b59b-25a6a5070690
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 894304081fb8206b2137c9ed6124b306111eb6cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855783"
---
# <a name="tutorial-azure-active-directory-integration-with-workpath"></a><span data-ttu-id="63147-103">Tutorial: Azure Active Directory integration with Workpath</span><span class="sxs-lookup"><span data-stu-id="63147-103">Tutorial: Azure Active Directory integration with Workpath</span></span>

<span data-ttu-id="63147-104">In this tutorial, you learn how to integrate Workpath with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="63147-104">In this tutorial, you learn how to integrate Workpath with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="63147-105">Integrating Workpath with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="63147-105">Integrating Workpath with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="63147-106">You can control in Azure AD who has access to Workpath</span><span class="sxs-lookup"><span data-stu-id="63147-106">You can control in Azure AD who has access to Workpath</span></span>
- <span data-ttu-id="63147-107">You can enable your users to automatically get signed-on to Workpath (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="63147-107">You can enable your users to automatically get signed-on to Workpath (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="63147-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="63147-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="63147-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="63147-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63147-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="63147-110">Prerequisites</span></span>

<span data-ttu-id="63147-111">To configure Azure AD integration with Workpath, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="63147-111">To configure Azure AD integration with Workpath, you need the following items:</span></span>

- <span data-ttu-id="63147-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="63147-112">An Azure AD subscription</span></span>
- <span data-ttu-id="63147-113">A Workpath single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="63147-113">A Workpath single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="63147-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="63147-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="63147-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="63147-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="63147-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="63147-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="63147-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="63147-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="63147-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="63147-118">Scenario description</span></span>
<span data-ttu-id="63147-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="63147-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="63147-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="63147-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="63147-121">Adding Workpath from the gallery</span><span class="sxs-lookup"><span data-stu-id="63147-121">Adding Workpath from the gallery</span></span>
1. <span data-ttu-id="63147-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="63147-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workpath-from-the-gallery"></a><span data-ttu-id="63147-123">Adding Workpath from the gallery</span><span class="sxs-lookup"><span data-stu-id="63147-123">Adding Workpath from the gallery</span></span>
<span data-ttu-id="63147-124">To configure the integration of Workpath into Azure AD, you need to add Workpath from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="63147-124">To configure the integration of Workpath into Azure AD, you need to add Workpath from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="63147-125">**To add Workpath from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="63147-125">**To add Workpath from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="63147-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="63147-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="63147-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="63147-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="63147-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="63147-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="63147-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="63147-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="63147-133">In the search box, type **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="63147-133">In the search box, type **Workpath**.</span></span>

    ![Creating an Azure AD test user](./media/workpath-tutorial/tutorial_workpath_search.png)

1. <span data-ttu-id="63147-135">In the results panel, select **Workpath**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="63147-135">In the results panel, select **Workpath**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/workpath-tutorial/tutorial_workpath_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="63147-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="63147-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="63147-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="63147-138">In this section, you configure and test Azure AD single sign-on with Workpath based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="63147-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workpath is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="63147-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Workpath is to a user in Azure AD.</span></span> <span data-ttu-id="63147-140">In other words, a link relationship between an Azure AD user and the related user in Workpath needs to be established.</span><span class="sxs-lookup"><span data-stu-id="63147-140">In other words, a link relationship between an Azure AD user and the related user in Workpath needs to be established.</span></span>

<span data-ttu-id="63147-141">In Workpath, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="63147-141">In Workpath, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="63147-142">To configure and test Azure AD single sign-on with Workpath, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="63147-142">To configure and test Azure AD single sign-on with Workpath, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="63147-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="63147-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="63147-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63147-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="63147-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - to have a counterpart of Britta Simon in Workpath that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="63147-145">**[Creating a Workpath test user](#creating-a-workpath-test-user)** - to have a counterpart of Britta Simon in Workpath that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="63147-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="63147-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="63147-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="63147-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="63147-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="63147-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="63147-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workpath application.</span><span class="sxs-lookup"><span data-stu-id="63147-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workpath application.</span></span>

<span data-ttu-id="63147-150">**To configure Azure AD single sign-on with Workpath, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="63147-150">**To configure Azure AD single sign-on with Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="63147-151">In the Azure portal, on the **Workpath** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="63147-151">In the Azure portal, on the **Workpath** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="63147-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="63147-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/workpath-tutorial/tutorial_workpath_samlbase.png)

1. <span data-ttu-id="63147-155">On the **Workpath Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="63147-155">On the **Workpath Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/workpath-tutorial/tutorial_workpath_url.png)

    <span data-ttu-id="63147-157">a.</span><span class="sxs-lookup"><span data-stu-id="63147-157">a.</span></span> <span data-ttu-id="63147-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="63147-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/metadata/<instancename>`</span></span>

    <span data-ttu-id="63147-159">b.</span><span class="sxs-lookup"><span data-stu-id="63147-159">b.</span></span> <span data-ttu-id="63147-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="63147-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.workpath.com/v1/saml/assert/<instancename>`</span></span>

1. <span data-ttu-id="63147-161">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="63147-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="63147-162">If you wish to configure the application in **SP** initiated mode, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="63147-162">If you wish to configure the application in **SP** initiated mode, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/workpath-tutorial/tutorial_workpath_url1.png)

    <span data-ttu-id="63147-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.workpath.com/ `</span><span class="sxs-lookup"><span data-stu-id="63147-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.workpath.com/ `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="63147-165">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="63147-165">These values are not real.</span></span> <span data-ttu-id="63147-166">Update these values with the actual Sign-on URL, Identifier and Reply URL.</span><span class="sxs-lookup"><span data-stu-id="63147-166">Update these values with the actual Sign-on URL, Identifier and Reply URL.</span></span> <span data-ttu-id="63147-167">Contact [Workpath support team](https://help.workpath.com) to get these values.</span><span class="sxs-lookup"><span data-stu-id="63147-167">Contact [Workpath support team](https://help.workpath.com) to get these values.</span></span>

1. <span data-ttu-id="63147-168">Workpath application expects the SAML assertions in a specific format.</span><span class="sxs-lookup"><span data-stu-id="63147-168">Workpath application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="63147-169">Configure the following claims for this application.</span><span class="sxs-lookup"><span data-stu-id="63147-169">Configure the following claims for this application.</span></span> <span data-ttu-id="63147-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span><span class="sxs-lookup"><span data-stu-id="63147-170">You can manage the values of these attributes from the "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="63147-171">The following screenshot shows an example for this configuration.</span><span class="sxs-lookup"><span data-stu-id="63147-171">The following screenshot shows an example for this configuration.</span></span> 

    ![Configure Single Sign-On](./media/workpath-tutorial/tutorial_workpath_attributes.png)
    
1. <span data-ttu-id="63147-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="63147-173">In the **User Attributes** section on the **Single sign-on** dialog, configure SAML token attribute as shown in the image and perform the following steps:</span></span>
    
    | <span data-ttu-id="63147-174">Attribute Name</span><span class="sxs-lookup"><span data-stu-id="63147-174">Attribute Name</span></span> | <span data-ttu-id="63147-175">Attribute Value</span><span class="sxs-lookup"><span data-stu-id="63147-175">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="63147-176">first_name</span><span class="sxs-lookup"><span data-stu-id="63147-176">first_name</span></span> | <span data-ttu-id="63147-177">user.givenname</span><span class="sxs-lookup"><span data-stu-id="63147-177">user.givenname</span></span> |
    | <span data-ttu-id="63147-178">last_name</span><span class="sxs-lookup"><span data-stu-id="63147-178">last_name</span></span> | <span data-ttu-id="63147-179">user.surname</span><span class="sxs-lookup"><span data-stu-id="63147-179">user.surname</span></span> |
    
    <span data-ttu-id="63147-180">a.</span><span class="sxs-lookup"><span data-stu-id="63147-180">a.</span></span> <span data-ttu-id="63147-181">Click **Add attribute** to open the **Add Attribute** dialog.</span><span class="sxs-lookup"><span data-stu-id="63147-181">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Configure Single Sign-On](./media/workpath-tutorial/tutorial_attribute_04.png)

    <span data-ttu-id="63147-183">b.</span><span class="sxs-lookup"><span data-stu-id="63147-183">b.</span></span> <span data-ttu-id="63147-184">In the **Name** textbox, type the attribute name shown for that row.</span><span class="sxs-lookup"><span data-stu-id="63147-184">In the **Name** textbox, type the attribute name shown for that row.</span></span>

    ![Configure Single Sign-On](./media/workpath-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="63147-186">c.</span><span class="sxs-lookup"><span data-stu-id="63147-186">c.</span></span> <span data-ttu-id="63147-187">From the **Value** list, type the attribute value shown for that row.</span><span class="sxs-lookup"><span data-stu-id="63147-187">From the **Value** list, type the attribute value shown for that row.</span></span>

    <span data-ttu-id="63147-188">d.</span><span class="sxs-lookup"><span data-stu-id="63147-188">d.</span></span> <span data-ttu-id="63147-189">Leave the **Namespace** textbox blank.</span><span class="sxs-lookup"><span data-stu-id="63147-189">Leave the **Namespace** textbox blank.</span></span>
    
    <span data-ttu-id="63147-190">e.</span><span class="sxs-lookup"><span data-stu-id="63147-190">e.</span></span> <span data-ttu-id="63147-191">Click **Ok**.</span><span class="sxs-lookup"><span data-stu-id="63147-191">Click **Ok**.</span></span>
    

1. <span data-ttu-id="63147-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="63147-192">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/workpath-tutorial/tutorial_workpath_certificate.png) 

1. <span data-ttu-id="63147-194">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="63147-194">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/workpath-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="63147-196">On the **Workpath Configuration** section, click **Configure Workpath** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="63147-196">On the **Workpath Configuration** section, click **Configure Workpath** to open **Configure sign-on** window.</span></span> <span data-ttu-id="63147-197">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="63147-197">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/workpath-tutorial/tutorial_workpath_configure.png) 

1. <span data-ttu-id="63147-199">To configure single sign-on on **Workpath** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workpath support team](https://help.workpath.com).</span><span class="sxs-lookup"><span data-stu-id="63147-199">To configure single sign-on on **Workpath** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workpath support team](https://help.workpath.com).</span></span> 

> [!TIP]
> <span data-ttu-id="63147-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="63147-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="63147-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="63147-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="63147-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="63147-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="63147-203">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="63147-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="63147-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="63147-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="63147-206">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="63147-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="63147-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="63147-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/workpath-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="63147-209">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="63147-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/workpath-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="63147-211">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="63147-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/workpath-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="63147-213">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="63147-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/workpath-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="63147-215">a.</span><span class="sxs-lookup"><span data-stu-id="63147-215">a.</span></span> <span data-ttu-id="63147-216">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="63147-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="63147-217">b.</span><span class="sxs-lookup"><span data-stu-id="63147-217">b.</span></span> <span data-ttu-id="63147-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="63147-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="63147-219">c.</span><span class="sxs-lookup"><span data-stu-id="63147-219">c.</span></span> <span data-ttu-id="63147-220">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="63147-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="63147-221">d.</span><span class="sxs-lookup"><span data-stu-id="63147-221">d.</span></span> <span data-ttu-id="63147-222">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="63147-222">Click **Create**.</span></span>
 
### <a name="creating-a-workpath-test-user"></a><span data-ttu-id="63147-223">Creating a Workpath test user</span><span class="sxs-lookup"><span data-stu-id="63147-223">Creating a Workpath test user</span></span>

<span data-ttu-id="63147-224">Workpath supports Just in time user provisioning.</span><span class="sxs-lookup"><span data-stu-id="63147-224">Workpath supports Just in time user provisioning.</span></span> <span data-ttu-id="63147-225">After authentication users are created in the application automatically.</span><span class="sxs-lookup"><span data-stu-id="63147-225">After authentication users are created in the application automatically.</span></span> 


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="63147-226">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="63147-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="63147-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workpath.</span><span class="sxs-lookup"><span data-stu-id="63147-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workpath.</span></span>

![Assign User][200] 

<span data-ttu-id="63147-229">**To assign Britta Simon to Workpath, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="63147-229">**To assign Britta Simon to Workpath, perform the following steps:**</span></span>

1. <span data-ttu-id="63147-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="63147-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="63147-232">In the applications list, select **Workpath**.</span><span class="sxs-lookup"><span data-stu-id="63147-232">In the applications list, select **Workpath**.</span></span>

    ![Configure Single Sign-On](./media/workpath-tutorial/tutorial_workpath_app.png) 

1. <span data-ttu-id="63147-234">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="63147-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="63147-236">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="63147-236">Click **Add** button.</span></span> <span data-ttu-id="63147-237">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="63147-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="63147-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="63147-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="63147-240">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="63147-240">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="63147-241">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="63147-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="63147-242">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="63147-242">Testing single sign-on</span></span>

<span data-ttu-id="63147-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="63147-243">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="63147-244">When you click the Workpath tile in the Access Panel, you should get automatically signed-on to your Workpath application.</span><span class="sxs-lookup"><span data-stu-id="63147-244">When you click the Workpath tile in the Access Panel, you should get automatically signed-on to your Workpath application.</span></span>
<span data-ttu-id="63147-245">For more information about the Access Panel, see [introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="63147-245">For more information about the Access Panel, see [introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="63147-246">Additional resources</span><span class="sxs-lookup"><span data-stu-id="63147-246">Additional resources</span></span>

* [<span data-ttu-id="63147-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="63147-247">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="63147-248">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="63147-248">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/workpath-tutorial/tutorial_general_01.png
[2]: ./media/workpath-tutorial/tutorial_general_02.png
[3]: ./media/workpath-tutorial/tutorial_general_03.png
[4]: ./media/workpath-tutorial/tutorial_general_04.png

[100]: ./media/workpath-tutorial/tutorial_general_100.png

[200]: ./media/workpath-tutorial/tutorial_general_200.png
[201]: ./media/workpath-tutorial/tutorial_general_201.png
[202]: ./media/workpath-tutorial/tutorial_general_202.png
[203]: ./media/workpath-tutorial/tutorial_general_203.png

