---
title: 'Tutorial: Azure Active Directory integration with FreshDesk | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and FreshDesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: c2a3e5aa-7b5a-4fe4-9285-45dbe6e8efcc
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2018
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: db4750e01b62835cf08fd52e3288e94aea539b26
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856278"
---
# <a name="tutorial-azure-active-directory-integration-with-freshdesk"></a><span data-ttu-id="b7500-103">Tutorial: Azure Active Directory integration with FreshDesk</span><span class="sxs-lookup"><span data-stu-id="b7500-103">Tutorial: Azure Active Directory integration with FreshDesk</span></span>

<span data-ttu-id="b7500-104">In this tutorial, you learn how to integrate FreshDesk with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b7500-104">In this tutorial, you learn how to integrate FreshDesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b7500-105">Integrating FreshDesk with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="b7500-105">Integrating FreshDesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b7500-106">You can control in Azure AD who has access to FreshDesk</span><span class="sxs-lookup"><span data-stu-id="b7500-106">You can control in Azure AD who has access to FreshDesk</span></span>
- <span data-ttu-id="b7500-107">You can enable your users to automatically get signed-on to FreshDesk (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="b7500-107">You can enable your users to automatically get signed-on to FreshDesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b7500-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="b7500-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b7500-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="b7500-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7500-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b7500-110">Prerequisites</span></span>

<span data-ttu-id="b7500-111">To configure Azure AD integration with FreshDesk, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="b7500-111">To configure Azure AD integration with FreshDesk, you need the following items:</span></span>

- <span data-ttu-id="b7500-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="b7500-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b7500-113">A FreshDesk single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="b7500-113">A FreshDesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b7500-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="b7500-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b7500-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="b7500-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b7500-116">You should not use your production environment, unless this is necessary.</span><span class="sxs-lookup"><span data-stu-id="b7500-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b7500-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7500-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b7500-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="b7500-118">Scenario description</span></span>

<span data-ttu-id="b7500-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="b7500-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>
<span data-ttu-id="b7500-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="b7500-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7500-121">Adding FreshDesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="b7500-121">Adding FreshDesk from the gallery</span></span>
2. <span data-ttu-id="b7500-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b7500-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshdesk-from-the-gallery"></a><span data-ttu-id="b7500-123">Adding FreshDesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="b7500-123">Adding FreshDesk from the gallery</span></span>

<span data-ttu-id="b7500-124">To configure the integration of FreshDesk into Azure AD, you need to add FreshDesk from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="b7500-124">To configure the integration of FreshDesk into Azure AD, you need to add FreshDesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b7500-125">**To add FreshDesk from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7500-125">**To add FreshDesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b7500-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b7500-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b7500-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="b7500-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b7500-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b7500-129">Then go to **All applications**.</span></span>

    ![Applications][2]

3. <span data-ttu-id="b7500-131">Click **Add** button on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="b7500-131">Click **Add** button on the top of the dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="b7500-133">In the search box, type **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="b7500-133">In the search box, type **FreshDesk**.</span></span> <span data-ttu-id="b7500-134">Select **FreshDesk** from the results panel, and then select the **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="b7500-134">Select **FreshDesk** from the results panel, and then select the **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/freshdesk-tutorial/tutorial_freshdesk_addfromgallery.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b7500-136">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b7500-136">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="b7500-137">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="b7500-137">In this section, you configure and test Azure AD single sign-on with FreshDesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b7500-138">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshDesk is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b7500-138">For single sign-on to work, Azure AD needs to know what the counterpart user in FreshDesk is to a user in Azure AD.</span></span> <span data-ttu-id="b7500-139">In other words, a link relationship between an Azure AD user and the related user in FreshDesk needs to be established.</span><span class="sxs-lookup"><span data-stu-id="b7500-139">In other words, a link relationship between an Azure AD user and the related user in FreshDesk needs to be established.</span></span>

<span data-ttu-id="b7500-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="b7500-140">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in FreshDesk.</span></span>

<span data-ttu-id="b7500-141">To configure and test Azure AD single sign-on with FreshDesk, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="b7500-141">To configure and test Azure AD single sign-on with FreshDesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b7500-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="b7500-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b7500-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7500-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b7500-144">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - to have a counterpart of Britta Simon in FreshDesk that is linked to the Azure AD representation of her.</span><span class="sxs-lookup"><span data-stu-id="b7500-144">**[Creating a FreshDesk test user](#creating-a-freshdesk-test-user)** - to have a counterpart of Britta Simon in FreshDesk that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="b7500-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="b7500-145">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b7500-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="b7500-146">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b7500-147">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="b7500-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b7500-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FreshDesk application.</span><span class="sxs-lookup"><span data-stu-id="b7500-148">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FreshDesk application.</span></span>

<span data-ttu-id="b7500-149">**To configure Azure AD single sign-on with FreshDesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7500-149">**To configure Azure AD single sign-on with FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="b7500-150">In the Azure portal, on the **FreshDesk** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="b7500-150">In the Azure portal, on the **FreshDesk** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

2. <span data-ttu-id="b7500-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span><span class="sxs-lookup"><span data-stu-id="b7500-152">On the **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** to enable single sign on.</span></span>

    ![Configure Single Sign-On](./media/freshdesk-tutorial/tutorial_freshdesk_samlbase.png)

3. <span data-ttu-id="b7500-154">On the **FreshDesk Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b7500-154">On the **FreshDesk Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/freshdesk-tutorial/tutorial_freshdesk_url.png)

    <span data-ttu-id="b7500-156">a.</span><span class="sxs-lookup"><span data-stu-id="b7500-156">a.</span></span> <span data-ttu-id="b7500-157">In the **Sign on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span><span class="sxs-lookup"><span data-stu-id="b7500-157">In the **Sign on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.freshdesk.com` or any other value Freshdesk has suggested.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b7500-158">Please note that this is not the real value.</span><span class="sxs-lookup"><span data-stu-id="b7500-158">Please note that this is not the real value.</span></span> <span data-ttu-id="b7500-159">You have to update the value with the actual Sign-on URL.</span><span class="sxs-lookup"><span data-stu-id="b7500-159">You have to update the value with the actual Sign-on URL.</span></span> <span data-ttu-id="b7500-160">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span><span class="sxs-lookup"><span data-stu-id="b7500-160">Contact [FreshDesk Client support team](https://freshdesk.com/helpdesk-software?utm_source=Google-AdWords&utm_medium=Search-IND-Brand&utm_campaign=Search-IND-Brand&utm_term=freshdesk&device=c&gclid=COSH2_LH7NICFVUDvAodBPgBZg) to get this value.</span></span>  

4. <span data-ttu-id="b7500-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="b7500-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/freshdesk-tutorial/tutorial_freshdesk_certificate.png)

    > [!NOTE]
    > <span data-ttu-id="b7500-163">If you have any issues, please refer this [link](https://support.freshdesk.com/support/discussions/topics/317543).</span><span class="sxs-lookup"><span data-stu-id="b7500-163">If you have any issues, please refer this [link](https://support.freshdesk.com/support/discussions/topics/317543).</span></span>

5. <span data-ttu-id="b7500-164">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="b7500-164">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/freshdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b7500-166">Install **OpenSSL** in your system, if you have not installed in your system.</span><span class="sxs-lookup"><span data-stu-id="b7500-166">Install **OpenSSL** in your system, if you have not installed in your system.</span></span>

7. <span data-ttu-id="b7500-167">Open **Command Prompt** and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="b7500-167">Open **Command Prompt** and run the following commands:</span></span>

    <span data-ttu-id="b7500-168">a.</span><span class="sxs-lookup"><span data-stu-id="b7500-168">a.</span></span> <span data-ttu-id="b7500-169">Enter `openssl x509 -inform DER -in FreshDesk.cer -out certificate.crt` value in the command prompt.</span><span class="sxs-lookup"><span data-stu-id="b7500-169">Enter `openssl x509 -inform DER -in FreshDesk.cer -out certificate.crt` value in the command prompt.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b7500-170">Here **FreshDesk.cer** is the certificate which you have downloaded from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b7500-170">Here **FreshDesk.cer** is the certificate which you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="b7500-171">b.</span><span class="sxs-lookup"><span data-stu-id="b7500-171">b.</span></span> <span data-ttu-id="b7500-172">Enter `openssl x509 -noout -fingerprint -sha256 -inform pem -in certificate.crt` value in the command prompt.</span><span class="sxs-lookup"><span data-stu-id="b7500-172">Enter `openssl x509 -noout -fingerprint -sha256 -inform pem -in certificate.crt` value in the command prompt.</span></span> <span data-ttu-id="b7500-173">Here **certificate.crt** is the output certificate which is generated in the previous step.</span><span class="sxs-lookup"><span data-stu-id="b7500-173">Here **certificate.crt** is the output certificate which is generated in the previous step.</span></span>

    <span data-ttu-id="b7500-174">c.</span><span class="sxs-lookup"><span data-stu-id="b7500-174">c.</span></span> <span data-ttu-id="b7500-175">Copy the **Thumbprint** value and paste it into the Notepad.</span><span class="sxs-lookup"><span data-stu-id="b7500-175">Copy the **Thumbprint** value and paste it into the Notepad.</span></span> <span data-ttu-id="b7500-176">Remove colons from Thumbprint and obtain the final Thumbprint value.</span><span class="sxs-lookup"><span data-stu-id="b7500-176">Remove colons from Thumbprint and obtain the final Thumbprint value.</span></span>

8. <span data-ttu-id="b7500-177">On the **FreshDesk Configuration** section, click **Configure FreshDesk** to open Configure sign-on window.</span><span class="sxs-lookup"><span data-stu-id="b7500-177">On the **FreshDesk Configuration** section, click **Configure FreshDesk** to open Configure sign-on window.</span></span> <span data-ttu-id="b7500-178">Copy the SAML Single Sign-On Service URL and Sign-Out URL from the **Quick Reference** section.</span><span class="sxs-lookup"><span data-stu-id="b7500-178">Copy the SAML Single Sign-On Service URL and Sign-Out URL from the **Quick Reference** section.</span></span>

    ![Configure Single Sign-On](./media/freshdesk-tutorial/tutorial_freshdesk_configure.png)

9. <span data-ttu-id="b7500-180">In a different web browser window, log into your Freshdesk company site as an administrator.</span><span class="sxs-lookup"><span data-stu-id="b7500-180">In a different web browser window, log into your Freshdesk company site as an administrator.</span></span>

10. <span data-ttu-id="b7500-181">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="b7500-181">In the menu on the top, click **Admin**.</span></span>

    <span data-ttu-id="b7500-182">![Admin](./media/freshdesk-tutorial/IC776768.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="b7500-182">![Admin](./media/freshdesk-tutorial/IC776768.png "Admin")</span></span>

11. <span data-ttu-id="b7500-183">In the **General Settings** tab, click **Security**.</span><span class="sxs-lookup"><span data-stu-id="b7500-183">In the **General Settings** tab, click **Security**.</span></span>
  
    <span data-ttu-id="b7500-184">![Security](./media/freshdesk-tutorial/IC776769.png "Security")</span><span class="sxs-lookup"><span data-stu-id="b7500-184">![Security](./media/freshdesk-tutorial/IC776769.png "Security")</span></span>

12. <span data-ttu-id="b7500-185">In the **Security** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b7500-185">In the **Security** section, perform the following steps:</span></span>

    <span data-ttu-id="b7500-186">![Single Sign On](./media/freshdesk-tutorial/IC776770.png "Single Sign On")</span><span class="sxs-lookup"><span data-stu-id="b7500-186">![Single Sign On](./media/freshdesk-tutorial/IC776770.png "Single Sign On")</span></span>
  
    <span data-ttu-id="b7500-187">a.</span><span class="sxs-lookup"><span data-stu-id="b7500-187">a.</span></span> <span data-ttu-id="b7500-188">For **Single Sign On (SSO)**, select **On**.</span><span class="sxs-lookup"><span data-stu-id="b7500-188">For **Single Sign On (SSO)**, select **On**.</span></span>

    <span data-ttu-id="b7500-189">b.</span><span class="sxs-lookup"><span data-stu-id="b7500-189">b.</span></span> <span data-ttu-id="b7500-190">Select **SAML SSO**.</span><span class="sxs-lookup"><span data-stu-id="b7500-190">Select **SAML SSO**.</span></span>

    <span data-ttu-id="b7500-191">c.</span><span class="sxs-lookup"><span data-stu-id="b7500-191">c.</span></span> <span data-ttu-id="b7500-192">In the **SAML Login URL** textbox, paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b7500-192">In the **SAML Login URL** textbox, paste **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="b7500-193">d.</span><span class="sxs-lookup"><span data-stu-id="b7500-193">d.</span></span> <span data-ttu-id="b7500-194">In the **Logout URL** textbox, paste **Sign-Out URL** value, which you have copied from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b7500-194">In the **Logout URL** textbox, paste **Sign-Out URL** value, which you have copied from the Azure portal.</span></span>

    <span data-ttu-id="b7500-195">e.</span><span class="sxs-lookup"><span data-stu-id="b7500-195">e.</span></span> <span data-ttu-id="b7500-196">In the **Security Certificate Fingerprint** textbox, paste **Thumbprint** value which you have obtained earlier after removing the colons.</span><span class="sxs-lookup"><span data-stu-id="b7500-196">In the **Security Certificate Fingerprint** textbox, paste **Thumbprint** value which you have obtained earlier after removing the colons.</span></span>
  
    <span data-ttu-id="b7500-197">f.</span><span class="sxs-lookup"><span data-stu-id="b7500-197">f.</span></span> <span data-ttu-id="b7500-198">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b7500-198">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b7500-199">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b7500-199">Creating an Azure AD test user</span></span>

<span data-ttu-id="b7500-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7500-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="b7500-202">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7500-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b7500-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="b7500-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/freshdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b7500-205">Go to **Users and groups** and click **All users** to display the list of users.</span><span class="sxs-lookup"><span data-stu-id="b7500-205">Go to **Users and groups** and click **All users** to display the list of users.</span></span>

    ![Creating an Azure AD test user](./media/freshdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b7500-207">At the top of the dialog click **Add** to open the **User** dialog.</span><span class="sxs-lookup"><span data-stu-id="b7500-207">At the top of the dialog click **Add** to open the **User** dialog.</span></span>

    ![Creating an Azure AD test user](./media/freshdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b7500-209">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b7500-209">On the **User** dialog page, perform the following steps:</span></span>

    ![Creating an Azure AD test user](./media/freshdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b7500-211">a.</span><span class="sxs-lookup"><span data-stu-id="b7500-211">a.</span></span> <span data-ttu-id="b7500-212">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b7500-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b7500-213">b.</span><span class="sxs-lookup"><span data-stu-id="b7500-213">b.</span></span> <span data-ttu-id="b7500-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b7500-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b7500-215">c.</span><span class="sxs-lookup"><span data-stu-id="b7500-215">c.</span></span> <span data-ttu-id="b7500-216">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="b7500-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b7500-217">d.</span><span class="sxs-lookup"><span data-stu-id="b7500-217">d.</span></span> <span data-ttu-id="b7500-218">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b7500-218">Click **Create**.</span></span>

### <a name="creating-a-freshdesk-test-user"></a><span data-ttu-id="b7500-219">Creating a FreshDesk test user</span><span class="sxs-lookup"><span data-stu-id="b7500-219">Creating a FreshDesk test user</span></span>

<span data-ttu-id="b7500-220">In order to enable Azure AD users to log into FreshDesk, they must be provisioned into FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="b7500-220">In order to enable Azure AD users to log into FreshDesk, they must be provisioned into FreshDesk.</span></span>  
<span data-ttu-id="b7500-221">In the case of FreshDesk, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="b7500-221">In the case of FreshDesk, provisioning is a manual task.</span></span>

<span data-ttu-id="b7500-222">**To provision a user accounts, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7500-222">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="b7500-223">Log in to your **Freshdesk** tenant.</span><span class="sxs-lookup"><span data-stu-id="b7500-223">Log in to your **Freshdesk** tenant.</span></span>

2. <span data-ttu-id="b7500-224">In the menu on the top, click **Admin**.</span><span class="sxs-lookup"><span data-stu-id="b7500-224">In the menu on the top, click **Admin**.</span></span>

   <span data-ttu-id="b7500-225">![Admin](./media/freshdesk-tutorial/IC776772.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="b7500-225">![Admin](./media/freshdesk-tutorial/IC776772.png "Admin")</span></span>

3. <span data-ttu-id="b7500-226">In the **General Settings** tab, click **Agents**.</span><span class="sxs-lookup"><span data-stu-id="b7500-226">In the **General Settings** tab, click **Agents**.</span></span>
  
   <span data-ttu-id="b7500-227">![Agents](./media/freshdesk-tutorial/IC776773.png "Agents")</span><span class="sxs-lookup"><span data-stu-id="b7500-227">![Agents](./media/freshdesk-tutorial/IC776773.png "Agents")</span></span>

4. <span data-ttu-id="b7500-228">Click **New Agent**.</span><span class="sxs-lookup"><span data-stu-id="b7500-228">Click **New Agent**.</span></span>

    <span data-ttu-id="b7500-229">![New Agent](./media/freshdesk-tutorial/IC776774.png "New Agent")</span><span class="sxs-lookup"><span data-stu-id="b7500-229">![New Agent](./media/freshdesk-tutorial/IC776774.png "New Agent")</span></span>

5. <span data-ttu-id="b7500-230">On the Agent Information dialog, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b7500-230">On the Agent Information dialog, perform the following steps:</span></span>

   <span data-ttu-id="b7500-231">![Agent Information](./media/freshdesk-tutorial/IC776775.png "Agent Information")</span><span class="sxs-lookup"><span data-stu-id="b7500-231">![Agent Information](./media/freshdesk-tutorial/IC776775.png "Agent Information")</span></span>

   <span data-ttu-id="b7500-232">a.</span><span class="sxs-lookup"><span data-stu-id="b7500-232">a.</span></span> <span data-ttu-id="b7500-233">In the **Full Name** textbox, type the name of the Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="b7500-233">In the **Full Name** textbox, type the name of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="b7500-234">b.</span><span class="sxs-lookup"><span data-stu-id="b7500-234">b.</span></span> <span data-ttu-id="b7500-235">In the **Email** textbox, type the Azure AD email address of the Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="b7500-235">In the **Email** textbox, type the Azure AD email address of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="b7500-236">c.</span><span class="sxs-lookup"><span data-stu-id="b7500-236">c.</span></span> <span data-ttu-id="b7500-237">In the **Title** textbox, type the title of the Azure AD account you want to provision.</span><span class="sxs-lookup"><span data-stu-id="b7500-237">In the **Title** textbox, type the title of the Azure AD account you want to provision.</span></span>

   <span data-ttu-id="b7500-238">d.</span><span class="sxs-lookup"><span data-stu-id="b7500-238">d.</span></span> <span data-ttu-id="b7500-239">Select **Agents role**, and then click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="b7500-239">Select **Agents role**, and then click **Assign**.</span></span>

   <span data-ttu-id="b7500-240">e.</span><span class="sxs-lookup"><span data-stu-id="b7500-240">e.</span></span> <span data-ttu-id="b7500-241">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b7500-241">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b7500-242">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span><span class="sxs-lookup"><span data-stu-id="b7500-242">The Azure AD account holder will get an email that includes a link to confirm the account before it is activated.</span></span>
    >
    >[!NOTE]
    ><span data-ttu-id="b7500-243">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk to provision AAD user accounts.</span><span class="sxs-lookup"><span data-stu-id="b7500-243">You can use any other Freshdesk user account creation tools or APIs provided by Freshdesk to provision AAD user accounts.</span></span>
    <span data-ttu-id="b7500-244">to FreshDesk.</span><span class="sxs-lookup"><span data-stu-id="b7500-244">to FreshDesk.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b7500-245">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="b7500-245">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b7500-246">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Box.</span><span class="sxs-lookup"><span data-stu-id="b7500-246">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to Box.</span></span>

![Assign User][200]

<span data-ttu-id="b7500-248">**To assign Britta Simon to FreshDesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="b7500-248">**To assign Britta Simon to FreshDesk, perform the following steps:**</span></span>

1. <span data-ttu-id="b7500-249">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="b7500-249">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201]

2. <span data-ttu-id="b7500-251">In the applications list, select **FreshDesk**.</span><span class="sxs-lookup"><span data-stu-id="b7500-251">In the applications list, select **FreshDesk**.</span></span>

    ![Configure Single Sign-On](./media/freshdesk-tutorial/tutorial_freshdesk_app.png) 

3. <span data-ttu-id="b7500-253">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="b7500-253">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202]

4. <span data-ttu-id="b7500-255">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="b7500-255">Click **Add** button.</span></span> <span data-ttu-id="b7500-256">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b7500-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

5. <span data-ttu-id="b7500-258">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="b7500-258">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b7500-259">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="b7500-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b7500-260">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="b7500-260">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="b7500-261">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="b7500-261">Testing single sign-on</span></span>

<span data-ttu-id="b7500-262">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="b7500-262">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b7500-263">When you click the FreshDesk tile in the Access Panel, you should get login page to get signed-on to your FreshDesk application.</span><span class="sxs-lookup"><span data-stu-id="b7500-263">When you click the FreshDesk tile in the Access Panel, you should get login page to get signed-on to your FreshDesk application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b7500-264">Additional resources</span><span class="sxs-lookup"><span data-stu-id="b7500-264">Additional resources</span></span>

* [<span data-ttu-id="b7500-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b7500-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="b7500-266">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b7500-266">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/freshdesk-tutorial/tutorial_general_01.png
[2]: ./media/freshdesk-tutorial/tutorial_general_02.png
[3]: ./media/freshdesk-tutorial/tutorial_general_03.png
[4]: ./media/freshdesk-tutorial/tutorial_general_04.png

[100]: ./media/freshdesk-tutorial/tutorial_general_100.png

[200]: ./media/freshdesk-tutorial/tutorial_general_200.png
[201]: ./media/freshdesk-tutorial/tutorial_general_201.png
[202]: ./media/freshdesk-tutorial/tutorial_general_202.png
[203]: ./media/freshdesk-tutorial/tutorial_general_203.png