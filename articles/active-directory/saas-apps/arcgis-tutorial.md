---
title: 'Tutorial: Azure Active Directory integration with ArcGIS Online | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and ArcGIS Online.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a9e132a4-29e7-48bf-beb9-4148e617c8a9
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/13/2017
ms.author: jeedes
ms.openlocfilehash: 24a82bbaf47153791da2f21a0b68c2f81c0670e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856778"
---
# <a name="tutorial-azure-active-directory-integration-with-arcgis-online"></a><span data-ttu-id="62fe9-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span><span class="sxs-lookup"><span data-stu-id="62fe9-103">Tutorial: Azure Active Directory integration with ArcGIS Online</span></span>

<span data-ttu-id="62fe9-104">In this tutorial, you learn how to integrate ArcGIS Online with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62fe9-104">In this tutorial, you learn how to integrate ArcGIS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62fe9-105">Integrating ArcGIS Online with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="62fe9-105">Integrating ArcGIS Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="62fe9-106">You can control in Azure AD who has access to ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="62fe9-106">You can control in Azure AD who has access to ArcGIS Online.</span></span>
- <span data-ttu-id="62fe9-107">You can enable your users to automatically get signed-on to ArcGIS Online (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="62fe9-107">You can enable your users to automatically get signed-on to ArcGIS Online (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="62fe9-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="62fe9-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="62fe9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="62fe9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62fe9-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="62fe9-110">Prerequisites</span></span>

<span data-ttu-id="62fe9-111">To configure Azure AD integration with ArcGIS Online, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="62fe9-111">To configure Azure AD integration with ArcGIS Online, you need the following items:</span></span>

- <span data-ttu-id="62fe9-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="62fe9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62fe9-113">A ArcGIS Online single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="62fe9-113">A ArcGIS Online single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62fe9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="62fe9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62fe9-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="62fe9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62fe9-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="62fe9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62fe9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62fe9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62fe9-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="62fe9-118">Scenario description</span></span>
<span data-ttu-id="62fe9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="62fe9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62fe9-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="62fe9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62fe9-121">Adding ArcGIS Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="62fe9-121">Adding ArcGIS Online from the gallery</span></span>
1. <span data-ttu-id="62fe9-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="62fe9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-arcgis-online-from-the-gallery"></a><span data-ttu-id="62fe9-123">Adding ArcGIS Online from the gallery</span><span class="sxs-lookup"><span data-stu-id="62fe9-123">Adding ArcGIS Online from the gallery</span></span>
<span data-ttu-id="62fe9-124">To configure the integration of ArcGIS Online into Azure AD, you need to add ArcGIS Online from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="62fe9-124">To configure the integration of ArcGIS Online into Azure AD, you need to add ArcGIS Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="62fe9-125">**To add ArcGIS Online from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="62fe9-125">**To add ArcGIS Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="62fe9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="62fe9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="62fe9-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="62fe9-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="62fe9-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="62fe9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="62fe9-133">In the search box, type **ArcGIS Online**, select **ArcGIS Online** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="62fe9-133">In the search box, type **ArcGIS Online**, select **ArcGIS Online** from result panel then click **Add** button to add the application.</span></span>

    ![ArcGIS Online in the results list](./media/arcgis-tutorial/tutorial_arcgisonline_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="62fe9-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="62fe9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="62fe9-136">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="62fe9-136">In this section, you configure and test Azure AD single sign-on with ArcGIS Online based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62fe9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Online is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62fe9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ArcGIS Online is to a user in Azure AD.</span></span> <span data-ttu-id="62fe9-138">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Online needs to be established.</span><span class="sxs-lookup"><span data-stu-id="62fe9-138">In other words, a link relationship between an Azure AD user and the related user in ArcGIS Online needs to be established.</span></span>

<span data-ttu-id="62fe9-139">In ArcGIS Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="62fe9-139">In ArcGIS Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="62fe9-140">To configure and test Azure AD single sign-on with ArcGIS Online, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="62fe9-140">To configure and test Azure AD single sign-on with ArcGIS Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="62fe9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="62fe9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="62fe9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62fe9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="62fe9-143">**[Create a ArcGIS Online test user](#create-a-arcgis-online-test-user)** - to have a counterpart of Britta Simon in ArcGIS Online that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="62fe9-143">**[Create a ArcGIS Online test user](#create-a-arcgis-online-test-user)** - to have a counterpart of Britta Simon in ArcGIS Online that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="62fe9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="62fe9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="62fe9-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="62fe9-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="62fe9-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="62fe9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="62fe9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Online application.</span><span class="sxs-lookup"><span data-stu-id="62fe9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ArcGIS Online application.</span></span>

<span data-ttu-id="62fe9-148">**To configure Azure AD single sign-on with ArcGIS Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="62fe9-148">**To configure Azure AD single sign-on with ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="62fe9-149">In the Azure portal, on the **ArcGIS Online** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-149">In the Azure portal, on the **ArcGIS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="62fe9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="62fe9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/arcgis-tutorial/tutorial_arcgisonline_samlbase.png)

1. <span data-ttu-id="62fe9-153">On the **ArcGIS Online Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="62fe9-153">On the **ArcGIS Online Domain and URLs** section, perform the following steps:</span></span>

    ![ArcGIS Online Domain and URLs single sign-on information](./media/arcgis-tutorial/tutorial_arcgisonline_url.png)

    <span data-ttu-id="62fe9-155">a.</span><span class="sxs-lookup"><span data-stu-id="62fe9-155">a.</span></span> <span data-ttu-id="62fe9-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="62fe9-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.maps.arcgis.com`</span></span>

    <span data-ttu-id="62fe9-157">b.</span><span class="sxs-lookup"><span data-stu-id="62fe9-157">b.</span></span> <span data-ttu-id="62fe9-158">In the **Identifier** textbox, type a URL using the following pattern: `<companyname>.maps.arcgis.com`</span><span class="sxs-lookup"><span data-stu-id="62fe9-158">In the **Identifier** textbox, type a URL using the following pattern: `<companyname>.maps.arcgis.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="62fe9-159">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="62fe9-159">These values are not real.</span></span> <span data-ttu-id="62fe9-160">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="62fe9-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="62fe9-161">Contact [ArcGIS Online Client support team](http://support.esri.com/en/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="62fe9-161">Contact [ArcGIS Online Client support team](http://support.esri.com/en/) to get these values.</span></span> 
 


1. <span data-ttu-id="62fe9-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="62fe9-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/arcgis-tutorial/tutorial_arcgisonline_certificate.png) 

1. <span data-ttu-id="62fe9-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="62fe9-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/arcgis-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="62fe9-166">In a different web browser window, log into your ArcGIS company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="62fe9-166">In a different web browser window, log into your ArcGIS company site as an administrator.</span></span>

1. <span data-ttu-id="62fe9-167">Click **EDIT SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-167">Click **EDIT SETTINGS**.</span></span>

    <span data-ttu-id="62fe9-168">![Edit Settings](./media/arcgis-tutorial/ic784742.png "Edit Settings")</span><span class="sxs-lookup"><span data-stu-id="62fe9-168">![Edit Settings](./media/arcgis-tutorial/ic784742.png "Edit Settings")</span></span>

1. <span data-ttu-id="62fe9-169">Click **Security**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-169">Click **Security**.</span></span>

    <span data-ttu-id="62fe9-170">![Security](./media/arcgis-tutorial/ic784743.png "Security")</span><span class="sxs-lookup"><span data-stu-id="62fe9-170">![Security](./media/arcgis-tutorial/ic784743.png "Security")</span></span>

1. <span data-ttu-id="62fe9-171">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-171">Under **Enterprise Logins**, click **SET IDENTITY PROVIDER**.</span></span>

    <span data-ttu-id="62fe9-172">![Enterprise Logins](./media/arcgis-tutorial/ic784744.png "Enterprise Logins")</span><span class="sxs-lookup"><span data-stu-id="62fe9-172">![Enterprise Logins](./media/arcgis-tutorial/ic784744.png "Enterprise Logins")</span></span>

1. <span data-ttu-id="62fe9-173">On the **Set Identity Provider** configuration page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="62fe9-173">On the **Set Identity Provider** configuration page, perform the following steps:</span></span>
   
    <span data-ttu-id="62fe9-174">![Set Identity Provider](./media/arcgis-tutorial/ic784745.png "Set Identity Provider")</span><span class="sxs-lookup"><span data-stu-id="62fe9-174">![Set Identity Provider](./media/arcgis-tutorial/ic784745.png "Set Identity Provider")</span></span>
   
    <span data-ttu-id="62fe9-175">a.</span><span class="sxs-lookup"><span data-stu-id="62fe9-175">a.</span></span> <span data-ttu-id="62fe9-176">In the **Name** textbox, type your organization’s name.</span><span class="sxs-lookup"><span data-stu-id="62fe9-176">In the **Name** textbox, type your organization’s name.</span></span>

    <span data-ttu-id="62fe9-177">b.</span><span class="sxs-lookup"><span data-stu-id="62fe9-177">b.</span></span> <span data-ttu-id="62fe9-178">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-178">For **Metadata for the Enterprise Identity Provider will be supplied using**, select **A File**.</span></span>

    <span data-ttu-id="62fe9-179">c.</span><span class="sxs-lookup"><span data-stu-id="62fe9-179">c.</span></span> <span data-ttu-id="62fe9-180">To upload your downloaded metadata file, click **Choose file**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-180">To upload your downloaded metadata file, click **Choose file**.</span></span>

    <span data-ttu-id="62fe9-181">d.</span><span class="sxs-lookup"><span data-stu-id="62fe9-181">d.</span></span> <span data-ttu-id="62fe9-182">Click **SET IDENTITY PROVIDER**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-182">Click **SET IDENTITY PROVIDER**.</span></span>

> [!TIP]
> <span data-ttu-id="62fe9-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="62fe9-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="62fe9-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="62fe9-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="62fe9-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="62fe9-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="62fe9-186">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="62fe9-186">Create an Azure AD test user</span></span>

<span data-ttu-id="62fe9-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62fe9-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="62fe9-189">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="62fe9-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="62fe9-190">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="62fe9-190">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/arcgis-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="62fe9-192">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-192">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/arcgis-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="62fe9-194">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="62fe9-194">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/arcgis-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="62fe9-196">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="62fe9-196">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/arcgis-tutorial/create_aaduser_04.png)

    <span data-ttu-id="62fe9-198">a.</span><span class="sxs-lookup"><span data-stu-id="62fe9-198">a.</span></span> <span data-ttu-id="62fe9-199">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-199">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62fe9-200">b.</span><span class="sxs-lookup"><span data-stu-id="62fe9-200">b.</span></span> <span data-ttu-id="62fe9-201">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62fe9-201">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="62fe9-202">c.</span><span class="sxs-lookup"><span data-stu-id="62fe9-202">c.</span></span> <span data-ttu-id="62fe9-203">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="62fe9-203">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="62fe9-204">d.</span><span class="sxs-lookup"><span data-stu-id="62fe9-204">d.</span></span> <span data-ttu-id="62fe9-205">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-205">Click **Create**.</span></span>
 
### <a name="create-a-arcgis-online-test-user"></a><span data-ttu-id="62fe9-206">Create a ArcGIS Online test user</span><span class="sxs-lookup"><span data-stu-id="62fe9-206">Create a ArcGIS Online test user</span></span>

<span data-ttu-id="62fe9-207">In order to enable Azure AD users to log into ArcGIS Online, they must be provisioned into ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="62fe9-207">In order to enable Azure AD users to log into ArcGIS Online, they must be provisioned into ArcGIS Online.</span></span>  
<span data-ttu-id="62fe9-208">In the case of ArcGIS Online, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="62fe9-208">In the case of ArcGIS Online, provisioning is a manual task.</span></span>

<span data-ttu-id="62fe9-209">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="62fe9-209">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="62fe9-210">Log in to your **ArcGIS** tenant.</span><span class="sxs-lookup"><span data-stu-id="62fe9-210">Log in to your **ArcGIS** tenant.</span></span>

1. <span data-ttu-id="62fe9-211">Click **INVITE MEMBERS**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-211">Click **INVITE MEMBERS**.</span></span>
   
    <span data-ttu-id="62fe9-212">![Invite Members](./media/arcgis-tutorial/ic784747.png "Invite Members")</span><span class="sxs-lookup"><span data-stu-id="62fe9-212">![Invite Members](./media/arcgis-tutorial/ic784747.png "Invite Members")</span></span>

1. <span data-ttu-id="62fe9-213">Select **Add members automatically without sending an email**, and then click **NEXT**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-213">Select **Add members automatically without sending an email**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="62fe9-214">![Add Members Automatically](./media/arcgis-tutorial/ic784748.png "Add Members Automatically")</span><span class="sxs-lookup"><span data-stu-id="62fe9-214">![Add Members Automatically](./media/arcgis-tutorial/ic784748.png "Add Members Automatically")</span></span>

1. <span data-ttu-id="62fe9-215">On the **Members** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="62fe9-215">On the **Members** dialog page, perform the following steps:</span></span>
   
     <span data-ttu-id="62fe9-216">![Add and review](./media/arcgis-tutorial/ic784749.png "Add and review")</span><span class="sxs-lookup"><span data-stu-id="62fe9-216">![Add and review](./media/arcgis-tutorial/ic784749.png "Add and review")</span></span>
    
     <span data-ttu-id="62fe9-217">a.</span><span class="sxs-lookup"><span data-stu-id="62fe9-217">a.</span></span> <span data-ttu-id="62fe9-218">Enter the **Email**, **First Name**, and **Last Name** of a valid AAD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="62fe9-218">Enter the **Email**, **First Name**, and **Last Name** of a valid AAD account you want to provision.</span></span>
  
     <span data-ttu-id="62fe9-219">b.</span><span class="sxs-lookup"><span data-stu-id="62fe9-219">b.</span></span> <span data-ttu-id="62fe9-220">Click **ADD AND REVIEW**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-220">Click **ADD AND REVIEW**.</span></span>
1. <span data-ttu-id="62fe9-221">Review the data you have entered, and then click **ADD MEMBERS**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-221">Review the data you have entered, and then click **ADD MEMBERS**.</span></span>
   
    <span data-ttu-id="62fe9-222">![Add member](./media/arcgis-tutorial/ic784750.png "Add member")</span><span class="sxs-lookup"><span data-stu-id="62fe9-222">![Add member](./media/arcgis-tutorial/ic784750.png "Add member")</span></span>
        
    > [!NOTE]
    > <span data-ttu-id="62fe9-223">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span><span class="sxs-lookup"><span data-stu-id="62fe9-223">The Azure Active Directory account holder will receive an email and follow a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="62fe9-224">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="62fe9-224">Assign the Azure AD test user</span></span>

<span data-ttu-id="62fe9-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Online.</span><span class="sxs-lookup"><span data-stu-id="62fe9-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ArcGIS Online.</span></span>

![Assign the user role][200] 

<span data-ttu-id="62fe9-227">**To assign Britta Simon to ArcGIS Online, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="62fe9-227">**To assign Britta Simon to ArcGIS Online, perform the following steps:**</span></span>

1. <span data-ttu-id="62fe9-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="62fe9-230">In the applications list, select **ArcGIS Online**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-230">In the applications list, select **ArcGIS Online**.</span></span>

    ![The ArcGIS Online link in the Applications list](./media/arcgis-tutorial/tutorial_arcgisonline_app.png)  

1. <span data-ttu-id="62fe9-232">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="62fe9-232">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="62fe9-234">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="62fe9-234">Click **Add** button.</span></span> <span data-ttu-id="62fe9-235">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="62fe9-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="62fe9-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="62fe9-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="62fe9-238">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="62fe9-238">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="62fe9-239">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="62fe9-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="62fe9-240">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="62fe9-240">Test single sign-on</span></span>

<span data-ttu-id="62fe9-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="62fe9-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="62fe9-242">When you click the ArcGIS Online tile in the Access Panel, you should get automatically signed-on to your ArcGIS Online application.</span><span class="sxs-lookup"><span data-stu-id="62fe9-242">When you click the ArcGIS Online tile in the Access Panel, you should get automatically signed-on to your ArcGIS Online application.</span></span>
<span data-ttu-id="62fe9-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="62fe9-243">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="62fe9-244">Additional resources</span><span class="sxs-lookup"><span data-stu-id="62fe9-244">Additional resources</span></span>

* [<span data-ttu-id="62fe9-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62fe9-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="62fe9-246">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62fe9-246">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/arcgis-tutorial/tutorial_general_01.png
[2]: ./media/arcgis-tutorial/tutorial_general_02.png
[3]: ./media/arcgis-tutorial/tutorial_general_03.png
[4]: ./media/arcgis-tutorial/tutorial_general_04.png

[100]: ./media/arcgis-tutorial/tutorial_general_100.png

[200]: ./media/arcgis-tutorial/tutorial_general_200.png
[201]: ./media/arcgis-tutorial/tutorial_general_201.png
[202]: ./media/arcgis-tutorial/tutorial_general_202.png
[203]: ./media/arcgis-tutorial/tutorial_general_203.png

