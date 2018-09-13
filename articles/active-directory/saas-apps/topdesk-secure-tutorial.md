---
title: 'Tutorial: Azure Active Directory integration with TOPdesk - Secure | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and TOPdesk - Secure.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8e06ee33-18f9-4c05-9168-e6b162079d88
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2018
ms.author: jeedes
ms.openlocfilehash: 8529dfda5ee4a7fc3360f91163b7f5f5bbf6c6ff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868141"
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="8d741-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span><span class="sxs-lookup"><span data-stu-id="8d741-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>

<span data-ttu-id="8d741-104">In this tutorial, you learn how to integrate TOPdesk - Secure with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d741-104">In this tutorial, you learn how to integrate TOPdesk - Secure with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d741-105">Integrating TOPdesk - Secure with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="8d741-105">Integrating TOPdesk - Secure with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8d741-106">You can control in Azure AD who has access to TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="8d741-106">You can control in Azure AD who has access to TOPdesk - Secure.</span></span>
- <span data-ttu-id="8d741-107">You can enable your users to automatically get signed-on to TOPdesk - Secure (Single Sign-On) with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="8d741-107">You can enable your users to automatically get signed-on to TOPdesk - Secure (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="8d741-108">You can manage your accounts in one central location - the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8d741-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="8d741-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="8d741-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d741-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8d741-110">Prerequisites</span></span>

<span data-ttu-id="8d741-111">To configure Azure AD integration with TOPdesk - Secure, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="8d741-111">To configure Azure AD integration with TOPdesk - Secure, you need the following items:</span></span>

- <span data-ttu-id="8d741-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="8d741-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d741-113">A TOPdesk - Secure single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="8d741-113">A TOPdesk - Secure single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d741-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="8d741-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d741-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="8d741-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d741-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="8d741-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d741-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d741-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d741-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="8d741-118">Scenario description</span></span>

<span data-ttu-id="8d741-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="8d741-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d741-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="8d741-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d741-121">Adding TOPdesk - Secure from the gallery</span><span class="sxs-lookup"><span data-stu-id="8d741-121">Adding TOPdesk - Secure from the gallery</span></span>
1. <span data-ttu-id="8d741-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8d741-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-topdesk---secure-from-the-gallery"></a><span data-ttu-id="8d741-123">Adding TOPdesk - Secure from the gallery</span><span class="sxs-lookup"><span data-stu-id="8d741-123">Adding TOPdesk - Secure from the gallery</span></span>

<span data-ttu-id="8d741-124">To configure the integration of TOPdesk - Secure into Azure AD, you need to add TOPdesk - Secure from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="8d741-124">To configure the integration of TOPdesk - Secure into Azure AD, you need to add TOPdesk - Secure from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8d741-125">**To add TOPdesk - Secure from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d741-125">**To add TOPdesk - Secure from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8d741-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="8d741-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![The Azure Active Directory button][1]

2. <span data-ttu-id="8d741-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="8d741-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8d741-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8d741-129">Then go to **All applications**.</span></span>

    ![The Enterprise applications blade][2]

3. <span data-ttu-id="8d741-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="8d741-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![The New application button][3]

4. <span data-ttu-id="8d741-133">In the search box, type **TOPdesk - Secure**, select **TOPdesk - Secure** from result panel then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="8d741-133">In the search box, type **TOPdesk - Secure**, select **TOPdesk - Secure** from result panel then click **Add** button to add the application.</span></span>

    ![TOPdesk - Secure in the results list](./media/topdesk-secure-tutorial/tutorial_topdesk-secure_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="8d741-135">Configure and test Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8d741-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="8d741-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Secure based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="8d741-136">In this section, you configure and test Azure AD single sign-on with TOPdesk - Secure based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8d741-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TOPdesk - Secure is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d741-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TOPdesk - Secure is to a user in Azure AD.</span></span> <span data-ttu-id="8d741-138">In other words, a link relationship between an Azure AD user and the related user in TOPdesk - Secure needs to be established.</span><span class="sxs-lookup"><span data-stu-id="8d741-138">In other words, a link relationship between an Azure AD user and the related user in TOPdesk - Secure needs to be established.</span></span>

<span data-ttu-id="8d741-139">In TOPdesk - Secure, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="8d741-139">In TOPdesk - Secure, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8d741-140">To configure and test Azure AD single sign-on with TOPdesk - Secure, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="8d741-140">To configure and test Azure AD single sign-on with TOPdesk - Secure, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8d741-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="8d741-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8d741-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d741-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d741-143">**[Create a TOPdesk - Secure test user](#create-a-topdesk---secure-test-user)** - to have a counterpart of Britta Simon in TOPdesk - Secure that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="8d741-143">**[Create a TOPdesk - Secure test user](#create-a-topdesk---secure-test-user)** - to have a counterpart of Britta Simon in TOPdesk - Secure that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d741-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8d741-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d741-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="8d741-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="8d741-146">Configure Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="8d741-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="8d741-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TOPdesk - Secure application.</span><span class="sxs-lookup"><span data-stu-id="8d741-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TOPdesk - Secure application.</span></span>

<span data-ttu-id="8d741-148">**To configure Azure AD single sign-on with TOPdesk - Secure, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d741-148">**To configure Azure AD single sign-on with TOPdesk - Secure, perform the following steps:**</span></span>

1. <span data-ttu-id="8d741-149">In the Azure portal, on the **TOPdesk - Secure** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="8d741-149">In the Azure portal, on the **TOPdesk - Secure** application integration page, click **Single sign-on**.</span></span>

    ![Configure single sign-on link][4]

2. <span data-ttu-id="8d741-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="8d741-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>

    ![Single sign-on dialog box](./media/topdesk-secure-tutorial/tutorial_topdesk-secure_samlbase.png)

3. <span data-ttu-id="8d741-153">On the **TOPdesk - Secure Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d741-153">On the **TOPdesk - Secure Domain and URLs** section, perform the following steps:</span></span>

    ![TOPdesk - Secure Domain and URLs single sign-on information](./media/topdesk-secure-tutorial/tutorial_topdesk-secure_url.png)

    <span data-ttu-id="8d741-155">a.</span><span class="sxs-lookup"><span data-stu-id="8d741-155">a.</span></span> <span data-ttu-id="8d741-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net`</span><span class="sxs-lookup"><span data-stu-id="8d741-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net`</span></span>

    <span data-ttu-id="8d741-157">b.</span><span class="sxs-lookup"><span data-stu-id="8d741-157">b.</span></span> <span data-ttu-id="8d741-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/secure/login/verify`</span><span class="sxs-lookup"><span data-stu-id="8d741-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/secure/login/verify`</span></span>

    <span data-ttu-id="8d741-159">c.</span><span class="sxs-lookup"><span data-stu-id="8d741-159">c.</span></span> <span data-ttu-id="8d741-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span><span class="sxs-lookup"><span data-stu-id="8d741-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.topdesk.net/tas/public/login/saml`</span></span>

    > [!NOTE]
    > <span data-ttu-id="8d741-161">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="8d741-161">These values are not real.</span></span> <span data-ttu-id="8d741-162">Update these values with the actual Sign-On URL and Identifier.</span><span class="sxs-lookup"><span data-stu-id="8d741-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8d741-163">Reply URL is explained later in tutorial.</span><span class="sxs-lookup"><span data-stu-id="8d741-163">Reply URL is explained later in tutorial.</span></span> <span data-ttu-id="8d741-164">Contact [TOPdesk - Secure Client support team](http://www.topdesk.com/us/support) to get these values.</span><span class="sxs-lookup"><span data-stu-id="8d741-164">Contact [TOPdesk - Secure Client support team](http://www.topdesk.com/us/support) to get these values.</span></span> 

4. <span data-ttu-id="8d741-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="8d741-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![The Certificate download link](./media/topdesk-secure-tutorial/tutorial_topdesk-secure_certificate.png) 

5. <span data-ttu-id="8d741-167">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="8d741-167">Click **Save** button.</span></span>

    ![Configure Single Sign-On Save button](./media/topdesk-secure-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8d741-169">On the **TOPdesk - Secure Configuration** section, click **Configure TOPdesk - Secure** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="8d741-169">On the **TOPdesk - Secure Configuration** section, click **Configure TOPdesk - Secure** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8d741-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="8d741-170">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![TOPdesk - Secure Configuration](./media/topdesk-secure-tutorial/tutorial_topdesk-secure_configure.png)

7. <span data-ttu-id="8d741-172">Sign on to your **TOPdesk - Secure** company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="8d741-172">Sign on to your **TOPdesk - Secure** company site as an administrator.</span></span>

8. <span data-ttu-id="8d741-173">In the **TOPdesk** menu, click **Settings**.</span><span class="sxs-lookup"><span data-stu-id="8d741-173">In the **TOPdesk** menu, click **Settings**.</span></span>

    <span data-ttu-id="8d741-174">![Settings](./media/topdesk-secure-tutorial/ic790598.png "Settings")</span><span class="sxs-lookup"><span data-stu-id="8d741-174">![Settings](./media/topdesk-secure-tutorial/ic790598.png "Settings")</span></span>

9. <span data-ttu-id="8d741-175">Click **Login Settings**.</span><span class="sxs-lookup"><span data-stu-id="8d741-175">Click **Login Settings**.</span></span>

    <span data-ttu-id="8d741-176">![Login Settings](./media/topdesk-secure-tutorial/ic790599.png "Login Settings")</span><span class="sxs-lookup"><span data-stu-id="8d741-176">![Login Settings](./media/topdesk-secure-tutorial/ic790599.png "Login Settings")</span></span>

10. <span data-ttu-id="8d741-177">Expand the **Login Settings** menu, and then click **General**.</span><span class="sxs-lookup"><span data-stu-id="8d741-177">Expand the **Login Settings** menu, and then click **General**.</span></span>

    <span data-ttu-id="8d741-178">![General](./media/topdesk-secure-tutorial/ic790600.png "General")</span><span class="sxs-lookup"><span data-stu-id="8d741-178">![General](./media/topdesk-secure-tutorial/ic790600.png "General")</span></span>

11. <span data-ttu-id="8d741-179">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d741-179">In the **Secure** section of the **SAML login** configuration section, perform the following steps:</span></span>

    <span data-ttu-id="8d741-180">![Technical Settings](./media/topdesk-secure-tutorial/ic790855.png "Technical Settings")</span><span class="sxs-lookup"><span data-stu-id="8d741-180">![Technical Settings](./media/topdesk-secure-tutorial/ic790855.png "Technical Settings")</span></span>

    <span data-ttu-id="8d741-181">a.</span><span class="sxs-lookup"><span data-stu-id="8d741-181">a.</span></span> <span data-ttu-id="8d741-182">Click **Download** to download the public metadata file, and then save it locally on your computer.</span><span class="sxs-lookup"><span data-stu-id="8d741-182">Click **Download** to download the public metadata file, and then save it locally on your computer.</span></span>

    <span data-ttu-id="8d741-183">b.</span><span class="sxs-lookup"><span data-stu-id="8d741-183">b.</span></span> <span data-ttu-id="8d741-184">Open the metadata file, and then locate the **AssertionConsumerService** node.</span><span class="sxs-lookup"><span data-stu-id="8d741-184">Open the metadata file, and then locate the **AssertionConsumerService** node.</span></span>

    <span data-ttu-id="8d741-185">![Assertion Consumer Service](./media/topdesk-secure-tutorial/ic790856.png "Assertion Consumer Service")</span><span class="sxs-lookup"><span data-stu-id="8d741-185">![Assertion Consumer Service](./media/topdesk-secure-tutorial/ic790856.png "Assertion Consumer Service")</span></span>

    <span data-ttu-id="8d741-186">c.</span><span class="sxs-lookup"><span data-stu-id="8d741-186">c.</span></span> <span data-ttu-id="8d741-187">Copy the **AssertionConsumerService** value, paste this value in the Reply URL textbox in **TOPdesk - Secure Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="8d741-187">Copy the **AssertionConsumerService** value, paste this value in the Reply URL textbox in **TOPdesk - Secure Domain and URLs** section.</span></span>

12. <span data-ttu-id="8d741-188">To create a certificate file, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d741-188">To create a certificate file, perform the following steps:</span></span>

    <span data-ttu-id="8d741-189">![Certificate](./media/topdesk-secure-tutorial/ic790606.png "Certificate")</span><span class="sxs-lookup"><span data-stu-id="8d741-189">![Certificate](./media/topdesk-secure-tutorial/ic790606.png "Certificate")</span></span>

    <span data-ttu-id="8d741-190">a.</span><span class="sxs-lookup"><span data-stu-id="8d741-190">a.</span></span> <span data-ttu-id="8d741-191">Open the downloaded metadata file from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8d741-191">Open the downloaded metadata file from Azure portal.</span></span>

    <span data-ttu-id="8d741-192">b.</span><span class="sxs-lookup"><span data-stu-id="8d741-192">b.</span></span> <span data-ttu-id="8d741-193">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="8d741-193">Expand the **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>

    <span data-ttu-id="8d741-194">c.</span><span class="sxs-lookup"><span data-stu-id="8d741-194">c.</span></span> <span data-ttu-id="8d741-195">Copy the value of the **X509Certificate** node.</span><span class="sxs-lookup"><span data-stu-id="8d741-195">Copy the value of the **X509Certificate** node.</span></span>

    <span data-ttu-id="8d741-196">d.</span><span class="sxs-lookup"><span data-stu-id="8d741-196">d.</span></span> <span data-ttu-id="8d741-197">Save the copied **X509Certificate** value locally on your computer in a file.</span><span class="sxs-lookup"><span data-stu-id="8d741-197">Save the copied **X509Certificate** value locally on your computer in a file.</span></span>

13. <span data-ttu-id="8d741-198">In the **Public** section, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="8d741-198">In the **Public** section, click **Add**.</span></span>

    <span data-ttu-id="8d741-199">![Add](./media/topdesk-secure-tutorial/ic790607.png "Add")</span><span class="sxs-lookup"><span data-stu-id="8d741-199">![Add](./media/topdesk-secure-tutorial/ic790607.png "Add")</span></span>

14. <span data-ttu-id="8d741-200">On the **SAML configuration assistant** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d741-200">On the **SAML configuration assistant** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="8d741-201">![SAML Configuration Assistant](./media/topdesk-secure-tutorial/ic790608.png "SAML Configuration Assistant")</span><span class="sxs-lookup"><span data-stu-id="8d741-201">![SAML Configuration Assistant](./media/topdesk-secure-tutorial/ic790608.png "SAML Configuration Assistant")</span></span>

    <span data-ttu-id="8d741-202">a.</span><span class="sxs-lookup"><span data-stu-id="8d741-202">a.</span></span> <span data-ttu-id="8d741-203">To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="8d741-203">To upload your downloaded metadata file from Azure portal, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="8d741-204">b.</span><span class="sxs-lookup"><span data-stu-id="8d741-204">b.</span></span> <span data-ttu-id="8d741-205">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="8d741-205">To upload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="8d741-206">c.</span><span class="sxs-lookup"><span data-stu-id="8d741-206">c.</span></span> <span data-ttu-id="8d741-207">For **Private key(RSA, PKCS8, DER)**, you can upload your own private key or you can contact [TOPdesk - Secure Client support team](http://www.topdesk.com/us/support) to get the private key.</span><span class="sxs-lookup"><span data-stu-id="8d741-207">For **Private key(RSA, PKCS8, DER)**, you can upload your own private key or you can contact [TOPdesk - Secure Client support team](http://www.topdesk.com/us/support) to get the private key.</span></span>

    <span data-ttu-id="8d741-208">d.</span><span class="sxs-lookup"><span data-stu-id="8d741-208">d.</span></span> <span data-ttu-id="8d741-209">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="8d741-209">To upload the logo file you got from the TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="8d741-210">e.</span><span class="sxs-lookup"><span data-stu-id="8d741-210">e.</span></span> <span data-ttu-id="8d741-211">In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="8d741-211">In the **User name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="8d741-212">f.</span><span class="sxs-lookup"><span data-stu-id="8d741-212">f.</span></span> <span data-ttu-id="8d741-213">In the **Display name** textbox, type a name for your configuration.</span><span class="sxs-lookup"><span data-stu-id="8d741-213">In the **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="8d741-214">g.</span><span class="sxs-lookup"><span data-stu-id="8d741-214">g.</span></span> <span data-ttu-id="8d741-215">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8d741-215">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="8d741-216">Create an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8d741-216">Create an Azure AD test user</span></span>

<span data-ttu-id="8d741-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d741-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Create an Azure AD test user][100]

<span data-ttu-id="8d741-219">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d741-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8d741-220">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span><span class="sxs-lookup"><span data-stu-id="8d741-220">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![The Azure Active Directory button](./media/topdesk-secure-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="8d741-222">To display the list of users, go to **Users and groups**, and then click **All users**.</span><span class="sxs-lookup"><span data-stu-id="8d741-222">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![The "Users and groups" and "All users" links](./media/topdesk-secure-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="8d741-224">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span><span class="sxs-lookup"><span data-stu-id="8d741-224">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![The Add button](./media/topdesk-secure-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="8d741-226">In the **User** dialog box, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d741-226">In the **User** dialog box, perform the following steps:</span></span>

    ![The User dialog box](./media/topdesk-secure-tutorial/create_aaduser_04.png)

    <span data-ttu-id="8d741-228">a.</span><span class="sxs-lookup"><span data-stu-id="8d741-228">a.</span></span> <span data-ttu-id="8d741-229">In the **Name** box, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d741-229">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d741-230">b.</span><span class="sxs-lookup"><span data-stu-id="8d741-230">b.</span></span> <span data-ttu-id="8d741-231">In the **User name** box, type the email address of user Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8d741-231">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="8d741-232">c.</span><span class="sxs-lookup"><span data-stu-id="8d741-232">c.</span></span> <span data-ttu-id="8d741-233">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span><span class="sxs-lookup"><span data-stu-id="8d741-233">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="8d741-234">d.</span><span class="sxs-lookup"><span data-stu-id="8d741-234">d.</span></span> <span data-ttu-id="8d741-235">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8d741-235">Click **Create**.</span></span>

### <a name="create-a-topdesk---secure-test-user"></a><span data-ttu-id="8d741-236">Create a TOPdesk - Secure test user</span><span class="sxs-lookup"><span data-stu-id="8d741-236">Create a TOPdesk - Secure test user</span></span>

<span data-ttu-id="8d741-237">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="8d741-237">In order to enable Azure AD users to log into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="8d741-238">In the case of TOPdesk - Secure, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="8d741-238">In the case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="8d741-239">To configure user provisioning, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d741-239">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="8d741-240">Sign on to your **TOPdesk - Secure** company site as administrator.</span><span class="sxs-lookup"><span data-stu-id="8d741-240">Sign on to your **TOPdesk - Secure** company site as administrator.</span></span>

2. <span data-ttu-id="8d741-241">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span><span class="sxs-lookup"><span data-stu-id="8d741-241">In the menu on the top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>

    <span data-ttu-id="8d741-242">![Operator](./media/topdesk-secure-tutorial/ic790610.png "Operator")</span><span class="sxs-lookup"><span data-stu-id="8d741-242">![Operator](./media/topdesk-secure-tutorial/ic790610.png "Operator")</span></span>

3. <span data-ttu-id="8d741-243">On the **New Operator** dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8d741-243">On the **New Operator** dialog, perform the following steps:</span></span>

    <span data-ttu-id="8d741-244">![New Operator](./media/topdesk-secure-tutorial/ic790611.png "New Operator")</span><span class="sxs-lookup"><span data-stu-id="8d741-244">![New Operator](./media/topdesk-secure-tutorial/ic790611.png "New Operator")</span></span>

    <span data-ttu-id="8d741-245">a.</span><span class="sxs-lookup"><span data-stu-id="8d741-245">a.</span></span> <span data-ttu-id="8d741-246">Click the **General** tab.</span><span class="sxs-lookup"><span data-stu-id="8d741-246">Click the **General** tab.</span></span>

    <span data-ttu-id="8d741-247">b.</span><span class="sxs-lookup"><span data-stu-id="8d741-247">b.</span></span> <span data-ttu-id="8d741-248">In the **Surname** textbox, type Surname of the user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="8d741-248">In the **Surname** textbox, type Surname of the user like **Simon**.</span></span>

    <span data-ttu-id="8d741-249">c.</span><span class="sxs-lookup"><span data-stu-id="8d741-249">c.</span></span> <span data-ttu-id="8d741-250">Select a **Site** for the account in the **Location** section.</span><span class="sxs-lookup"><span data-stu-id="8d741-250">Select a **Site** for the account in the **Location** section.</span></span>

    <span data-ttu-id="8d741-251">d.</span><span class="sxs-lookup"><span data-stu-id="8d741-251">d.</span></span> <span data-ttu-id="8d741-252">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span><span class="sxs-lookup"><span data-stu-id="8d741-252">In the **Login Name** textbox of the **TOPdesk Login** section, type a login name for your user.</span></span>

    <span data-ttu-id="8d741-253">e.</span><span class="sxs-lookup"><span data-stu-id="8d741-253">e.</span></span> <span data-ttu-id="8d741-254">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8d741-254">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="8d741-255">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="8d741-255">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure to provision AAD user accounts.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="8d741-256">Assign the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="8d741-256">Assign the Azure AD test user</span></span>

<span data-ttu-id="8d741-257">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="8d741-257">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TOPdesk - Secure.</span></span>

![Assign the user role][200] 

<span data-ttu-id="8d741-259">**To assign Britta Simon to TOPdesk - Secure, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="8d741-259">**To assign Britta Simon to TOPdesk - Secure, perform the following steps:**</span></span>

1. <span data-ttu-id="8d741-260">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="8d741-260">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="8d741-262">In the applications list, select **TOPdesk - Secure**.</span><span class="sxs-lookup"><span data-stu-id="8d741-262">In the applications list, select **TOPdesk - Secure**.</span></span>

    ![The TOPdesk - Secure link in the Applications list](./media/topdesk-secure-tutorial/tutorial_topdesk-secure_app.png)  

3. <span data-ttu-id="8d741-264">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="8d741-264">In the menu on the left, click **Users and groups**.</span></span>

    ![The "Users and groups" link][202]

4. <span data-ttu-id="8d741-266">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="8d741-266">Click **Add** button.</span></span> <span data-ttu-id="8d741-267">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8d741-267">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![The Add Assignment pane][203]

5. <span data-ttu-id="8d741-269">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="8d741-269">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8d741-270">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="8d741-270">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d741-271">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="8d741-271">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="8d741-272">Test single sign-on</span><span class="sxs-lookup"><span data-stu-id="8d741-272">Test single sign-on</span></span>

<span data-ttu-id="8d741-273">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="8d741-273">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8d741-274">When you click the TOPdesk - Secure tile in the Access Panel, you should get automatically signed-on to your TOPdesk - Secure application.</span><span class="sxs-lookup"><span data-stu-id="8d741-274">When you click the TOPdesk - Secure tile in the Access Panel, you should get automatically signed-on to your TOPdesk - Secure application.</span></span>
<span data-ttu-id="8d741-275">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d741-275">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d741-276">Additional resources</span><span class="sxs-lookup"><span data-stu-id="8d741-276">Additional resources</span></span>

* [<span data-ttu-id="8d741-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d741-277">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="8d741-278">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d741-278">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/topdesk-secure-tutorial/tutorial_general_01.png
[2]: ./media/topdesk-secure-tutorial/tutorial_general_02.png
[3]: ./media/topdesk-secure-tutorial/tutorial_general_03.png
[4]: ./media/topdesk-secure-tutorial/tutorial_general_04.png

[100]: ./media/topdesk-secure-tutorial/tutorial_general_100.png

[200]: ./media/topdesk-secure-tutorial/tutorial_general_200.png
[201]: ./media/topdesk-secure-tutorial/tutorial_general_201.png
[202]: ./media/topdesk-secure-tutorial/tutorial_general_202.png
[203]: ./media/topdesk-secure-tutorial/tutorial_general_203.png