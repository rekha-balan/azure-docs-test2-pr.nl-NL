---
title: 'Tutorial: Azure Active Directory integration with Attendance Management Services | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Attendance Management Services.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1f56e612-728b-4203-a545-a81dc5efda00
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2018
ms.author: jeedes
ms.openlocfilehash: c5422c9894c66348d571b757e50073d2a5501c7b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871253"
---
# <a name="tutorial-azure-active-directory-integration-with-attendance-management-services"></a><span data-ttu-id="58ab0-103">Tutorial: Azure Active Directory integration with Attendance Management Services</span><span class="sxs-lookup"><span data-stu-id="58ab0-103">Tutorial: Azure Active Directory integration with Attendance Management Services</span></span>

<span data-ttu-id="58ab0-104">In this tutorial, you learn how to integrate Attendance Management Services with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="58ab0-104">In this tutorial, you learn how to integrate Attendance Management Services with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="58ab0-105">Integrating Attendance Management Services with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="58ab0-105">Integrating Attendance Management Services with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="58ab0-106">You can control in Azure AD who has access to Attendance Management Services.</span><span class="sxs-lookup"><span data-stu-id="58ab0-106">You can control in Azure AD who has access to Attendance Management Services.</span></span>
- <span data-ttu-id="58ab0-107">You can enable your users to automatically get signed-on to Attendance Management Services (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="58ab0-107">You can enable your users to automatically get signed-on to Attendance Management Services (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="58ab0-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="58ab0-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="58ab0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="58ab0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58ab0-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="58ab0-110">Prerequisites</span></span>

<span data-ttu-id="58ab0-111">To configure Azure AD integration with Attendance Management Services, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="58ab0-111">To configure Azure AD integration with Attendance Management Services, you need the following items:</span></span>

- <span data-ttu-id="58ab0-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="58ab0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="58ab0-113">An Attendance Management Services single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="58ab0-113">An Attendance Management Services single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="58ab0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="58ab0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="58ab0-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="58ab0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="58ab0-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="58ab0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="58ab0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="58ab0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="58ab0-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="58ab0-118">Scenario description</span></span>
<span data-ttu-id="58ab0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="58ab0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="58ab0-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="58ab0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="58ab0-121">Adding Attendance Management Services from the gallery</span><span class="sxs-lookup"><span data-stu-id="58ab0-121">Adding Attendance Management Services from the gallery</span></span>
1. <span data-ttu-id="58ab0-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="58ab0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-attendance-management-services-from-the-gallery"></a><span data-ttu-id="58ab0-123">Adding Attendance Management Services from the gallery</span><span class="sxs-lookup"><span data-stu-id="58ab0-123">Adding Attendance Management Services from the gallery</span></span>
<span data-ttu-id="58ab0-124">To configure the integration of Attendance Management Services into Azure AD, you need to add Attendance Management Services from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="58ab0-124">To configure the integration of Attendance Management Services into Azure AD, you need to add Attendance Management Services from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="58ab0-125">**To add Attendance Management Services from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="58ab0-125">**To add Attendance Management Services from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="58ab0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="58ab0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

1. <span data-ttu-id="58ab0-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="58ab0-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]
    
1. <span data-ttu-id="58ab0-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="58ab0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

1. <span data-ttu-id="58ab0-133">In the search box, type **Attendance Management Services**, select **Attendance Management Services** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="58ab0-133">In the search box, type **Attendance Management Services**, select **Attendance Management Services** from result panel then click **Add** button to add the application.</span></span>

    ![Attendance Management Services in the results list](./media/attendancemanagementservices-tutorial/tutorial_attendancemanagementservices_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="58ab0-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="58ab0-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="58ab0-136">In this section, you configure and test Azure AD single sign-on with Attendance Management Services based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="58ab0-136">In this section, you configure and test Azure AD single sign-on with Attendance Management Services based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="58ab0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Attendance Management Services is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58ab0-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Attendance Management Services is to a user in Azure AD.</span></span> <span data-ttu-id="58ab0-138">In other words, a link relationship between an Azure AD user and the related user in Attendance Management Services needs to be established.</span><span class="sxs-lookup"><span data-stu-id="58ab0-138">In other words, a link relationship between an Azure AD user and the related user in Attendance Management Services needs to be established.</span></span>

<span data-ttu-id="58ab0-139">To configure and test Azure AD single sign-on with Attendance Management Services, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="58ab0-139">To configure and test Azure AD single sign-on with Attendance Management Services, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="58ab0-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="58ab0-140">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="58ab0-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="58ab0-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="58ab0-142">**[Create an Attendance Management Services test user](#create-an-attendance-management-service-test-user)** - to have a counterpart of Britta Simon in Attendance Management Services that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="58ab0-142">**[Create an Attendance Management Services test user](#create-an-attendance-management-service-test-user)** - to have a counterpart of Britta Simon in Attendance Management Services that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="58ab0-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="58ab0-143">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="58ab0-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="58ab0-144">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="58ab0-145">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="58ab0-145">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="58ab0-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Attendance Management Services application.</span><span class="sxs-lookup"><span data-stu-id="58ab0-146">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Attendance Management Services application.</span></span>

<span data-ttu-id="58ab0-147">**To configure Azure AD single sign-on with Attendance Management Services, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="58ab0-147">**To configure Azure AD single sign-on with Attendance Management Services, perform the following steps:**</span></span>

1. <span data-ttu-id="58ab0-148">In the Azure portal, on the **Attendance Management Services** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-148">In the Azure portal, on the **Attendance Management Services** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

1. <span data-ttu-id="58ab0-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="58ab0-150">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Single sign-on dialog box](./media/attendancemanagementservices-tutorial/tutorial_attendancemanagementservices_samlbase.png)

1. <span data-ttu-id="58ab0-152">On the **Attendance Management Services Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="58ab0-152">On the **Attendance Management Services Domain and URLs** section, perform the following steps:</span></span>

    ![Attendance Management Services Domain and URLs single sign-on information](./media/attendancemanagementservices-tutorial/tutorial_attendancemanagementservices_url.png)

    <span data-ttu-id="58ab0-154">a.</span><span class="sxs-lookup"><span data-stu-id="58ab0-154">a.</span></span> <span data-ttu-id="58ab0-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://id.obc.jp/<tenant information >/`</span><span class="sxs-lookup"><span data-stu-id="58ab0-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://id.obc.jp/<tenant information >/`</span></span>

    <span data-ttu-id="58ab0-156">b.</span><span class="sxs-lookup"><span data-stu-id="58ab0-156">b.</span></span> <span data-ttu-id="58ab0-157">In the **Identifier** textbox, type a URL using the following pattern: `https://id.obc.jp/<tenant information >/`</span><span class="sxs-lookup"><span data-stu-id="58ab0-157">In the **Identifier** textbox, type a URL using the following pattern: `https://id.obc.jp/<tenant information >/`</span></span>

    > [!NOTE]
    > <span data-ttu-id="58ab0-158">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="58ab0-158">These values are not real.</span></span> <span data-ttu-id="58ab0-159">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="58ab0-159">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="58ab0-160">Contact [Attendance Management Services Client support team](http://www.obcnet.jp/) to get these values.</span><span class="sxs-lookup"><span data-stu-id="58ab0-160">Contact [Attendance Management Services Client support team](http://www.obcnet.jp/) to get these values.</span></span>

1. <span data-ttu-id="58ab0-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="58ab0-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![The Certificate download link](./media/attendancemanagementservices-tutorial/tutorial_attendancemanagementservices_certificate.png) 

1. <span data-ttu-id="58ab0-163">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="58ab0-163">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/attendancemanagementservices-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="58ab0-165">On the **Attendance Management Services Configuration** section, click **Configure Attendance Management Services** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="58ab0-165">On the **Attendance Management Services Configuration** section, click **Configure Attendance Management Services** to open **Configure sign-on** window.</span></span> <span data-ttu-id="58ab0-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="58ab0-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Attendance Management Services Configuration](./media/attendancemanagementservices-tutorial/tutorial_attendancemanagementservices_configure.png) 

1. <span data-ttu-id="58ab0-168">In a different browser window, sign-on to your Attendance Management Services company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="58ab0-168">In a different browser window, sign-on to your Attendance Management Services company site as administrator.</span></span>

1. <span data-ttu-id="58ab0-169">Click on **SAML authentication** under the **Security management section**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-169">Click on **SAML authentication** under the **Security management section**.</span></span>

    ![Attendance Management Services Configuration](./media/attendancemanagementservices-tutorial/user1.png)

1. <span data-ttu-id="58ab0-171">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="58ab0-171">Perform the following steps:</span></span>

    ![Attendance Management Services Configuration](./media/attendancemanagementservices-tutorial/user2.png)

    <span data-ttu-id="58ab0-173">a.</span><span class="sxs-lookup"><span data-stu-id="58ab0-173">a.</span></span> <span data-ttu-id="58ab0-174">Select **Use SAML authentication**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-174">Select **Use SAML authentication**.</span></span>

    <span data-ttu-id="58ab0-175">b.</span><span class="sxs-lookup"><span data-stu-id="58ab0-175">b.</span></span> <span data-ttu-id="58ab0-176">In the **Identifier** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="58ab0-176">In the **Identifier** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="58ab0-177">c.</span><span class="sxs-lookup"><span data-stu-id="58ab0-177">c.</span></span> <span data-ttu-id="58ab0-178">In the **Authentication endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="58ab0-178">In the **Authentication endpoint URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="58ab0-179">d.</span><span class="sxs-lookup"><span data-stu-id="58ab0-179">d.</span></span> <span data-ttu-id="58ab0-180">Click **Select a file** to upload the certificate which you downloaded from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="58ab0-180">Click **Select a file** to upload the certificate which you downloaded from Azure AD.</span></span>

    <span data-ttu-id="58ab0-181">e.</span><span class="sxs-lookup"><span data-stu-id="58ab0-181">e.</span></span> <span data-ttu-id="58ab0-182">Select **Disable password authentication**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-182">Select **Disable password authentication**.</span></span>

    <span data-ttu-id="58ab0-183">f.</span><span class="sxs-lookup"><span data-stu-id="58ab0-183">f.</span></span> <span data-ttu-id="58ab0-184">Click **Registration**</span><span class="sxs-lookup"><span data-stu-id="58ab0-184">Click **Registration**</span></span>

> [!TIP]
> <span data-ttu-id="58ab0-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="58ab0-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span> <span data-ttu-id="58ab0-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="58ab0-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="58ab0-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="58ab0-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="58ab0-188">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="58ab0-188">Create an Azure AD test user</span></span>

<span data-ttu-id="58ab0-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="58ab0-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="58ab0-191">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="58ab0-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="58ab0-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="58ab0-192">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/attendancemanagementservices-tutorial/create_aaduser_01.png)

1. <span data-ttu-id="58ab0-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-194">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/attendancemanagementservices-tutorial/create_aaduser_02.png)

1. <span data-ttu-id="58ab0-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="58ab0-196">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/attendancemanagementservices-tutorial/create_aaduser_03.png)

1. <span data-ttu-id="58ab0-198">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="58ab0-198">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/attendancemanagementservices-tutorial/create_aaduser_04.png)

    <span data-ttu-id="58ab0-200">a.</span><span class="sxs-lookup"><span data-stu-id="58ab0-200">a.</span></span> <span data-ttu-id="58ab0-201">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-201">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="58ab0-202">b.</span><span class="sxs-lookup"><span data-stu-id="58ab0-202">b.</span></span> <span data-ttu-id="58ab0-203">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="58ab0-203">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="58ab0-204">c.</span><span class="sxs-lookup"><span data-stu-id="58ab0-204">c.</span></span> <span data-ttu-id="58ab0-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="58ab0-205">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="58ab0-206">d.</span><span class="sxs-lookup"><span data-stu-id="58ab0-206">d.</span></span> <span data-ttu-id="58ab0-207">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-207">Click **Create**.</span></span>
 
### <a name="create-an-attendance-management-services-test-user"></a><span data-ttu-id="58ab0-208">Create an Attendance Management Services test user</span><span class="sxs-lookup"><span data-stu-id="58ab0-208">Create an Attendance Management Services test user</span></span>

<span data-ttu-id="58ab0-209">To enable Azure AD users to log in to Attendance Management Services, they must be provisioned into Attendance Management Services.</span><span class="sxs-lookup"><span data-stu-id="58ab0-209">To enable Azure AD users to log in to Attendance Management Services, they must be provisioned into Attendance Management Services.</span></span> <span data-ttu-id="58ab0-210">In the case of Attendance Management Services, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="58ab0-210">In the case of Attendance Management Services, provisioning is a manual task.</span></span>

<span data-ttu-id="58ab0-211">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="58ab0-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="58ab0-212">Log in to your Attendance Management Services company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="58ab0-212">Log in to your Attendance Management Services company site as an administrator.</span></span>

1. <span data-ttu-id="58ab0-213">Click on **User management** under the **Security management section**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-213">Click on **User management** under the **Security management section**.</span></span>

    ![Add Employee](./media/attendancemanagementservices-tutorial/user5.png)

1. <span data-ttu-id="58ab0-215">Click **New rules login**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-215">Click **New rules login**.</span></span>

    ![Add Employee](./media/attendancemanagementservices-tutorial/user3.png)

1. <span data-ttu-id="58ab0-217">In the **OBCiD information** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="58ab0-217">In the **OBCiD information** section, perform the following steps:</span></span>

    ![Add Employee](./media/attendancemanagementservices-tutorial/user4.png)

    <span data-ttu-id="58ab0-219">a.</span><span class="sxs-lookup"><span data-stu-id="58ab0-219">a.</span></span> <span data-ttu-id="58ab0-220">In the **OBCiD** textbox, type the email of user like **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-220">In the **OBCiD** textbox, type the email of user like **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="58ab0-221">b.</span><span class="sxs-lookup"><span data-stu-id="58ab0-221">b.</span></span> <span data-ttu-id="58ab0-222">In the **Password** textbox, type the password of user.</span><span class="sxs-lookup"><span data-stu-id="58ab0-222">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="58ab0-223">c.</span><span class="sxs-lookup"><span data-stu-id="58ab0-223">c.</span></span> <span data-ttu-id="58ab0-224">Click **Registration**</span><span class="sxs-lookup"><span data-stu-id="58ab0-224">Click **Registration**</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="58ab0-225">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="58ab0-225">Assign the Azure AD test user</span></span>

<span data-ttu-id="58ab0-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Attendance Management Services.</span><span class="sxs-lookup"><span data-stu-id="58ab0-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Attendance Management Services.</span></span>

![Assign the user role][200] 

<span data-ttu-id="58ab0-228">**To assign Britta Simon to Attendance Management Services, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="58ab0-228">**To assign Britta Simon to Attendance Management Services, perform the following steps:**</span></span>

1. <span data-ttu-id="58ab0-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-229">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="58ab0-231">In the applications list, select **Attendance Management Services**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-231">In the applications list, select **Attendance Management Services**.</span></span>

    ![The Attendance Management Services link in the Applications list](./media/attendancemanagementservices-tutorial/tutorial_attendancemanagementservices_app.png)  

1. <span data-ttu-id="58ab0-233">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="58ab0-233">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

1. <span data-ttu-id="58ab0-235">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="58ab0-235">Click **Add** button.</span></span> <span data-ttu-id="58ab0-236">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="58ab0-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

1. <span data-ttu-id="58ab0-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="58ab0-238">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="58ab0-239">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="58ab0-239">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="58ab0-240">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="58ab0-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="58ab0-241">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="58ab0-241">Test single sign-on</span></span>

<span data-ttu-id="58ab0-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="58ab0-242">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="58ab0-243">When you click the Attendance Management Services tile in the Access Panel, you should get automatically signed-on to your Attendance Management Services application.</span><span class="sxs-lookup"><span data-stu-id="58ab0-243">When you click the Attendance Management Services tile in the Access Panel, you should get automatically signed-on to your Attendance Management Services application.</span></span>
<span data-ttu-id="58ab0-244">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="58ab0-244">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="58ab0-245">Additional resources</span><span class="sxs-lookup"><span data-stu-id="58ab0-245">Additional resources</span></span>

* [<span data-ttu-id="58ab0-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="58ab0-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="58ab0-247">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="58ab0-247">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/attendancemanagementservices-tutorial/tutorial_general_01.png
[2]: ./media/attendancemanagementservices-tutorial/tutorial_general_02.png
[3]: ./media/attendancemanagementservices-tutorial/tutorial_general_03.png
[4]: ./media/attendancemanagementservices-tutorial/tutorial_general_04.png

[100]: ./media/attendancemanagementservices-tutorial/tutorial_general_100.png

[200]: ./media/attendancemanagementservices-tutorial/tutorial_general_200.png
[201]: ./media/attendancemanagementservices-tutorial/tutorial_general_201.png
[202]: ./media/attendancemanagementservices-tutorial/tutorial_general_202.png
[203]: ./media/attendancemanagementservices-tutorial/tutorial_general_203.png

