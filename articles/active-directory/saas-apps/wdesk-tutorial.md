---
title: 'Tutorial: Azure Active Directory integration with Wdesk | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Wdesk.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 06900a91-a326-4663-8ba6-69ae741a536e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 9ff4d38240bf44cdb3112730b6f6962feed09a6a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856646"
---
# <a name="tutorial-azure-active-directory-integration-with-wdesk"></a><span data-ttu-id="2b4ce-103">Tutorial: Azure Active Directory integration with Wdesk</span><span class="sxs-lookup"><span data-stu-id="2b4ce-103">Tutorial: Azure Active Directory integration with Wdesk</span></span>

<span data-ttu-id="2b4ce-104">In this tutorial, you learn how to integrate Wdesk with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2b4ce-104">In this tutorial, you learn how to integrate Wdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2b4ce-105">Integrating Wdesk with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-105">Integrating Wdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="2b4ce-106">You can control in Azure AD who has access to Wdesk</span><span class="sxs-lookup"><span data-stu-id="2b4ce-106">You can control in Azure AD who has access to Wdesk</span></span>
- <span data-ttu-id="2b4ce-107">You can enable your users to automatically get signed-on to Wdesk (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="2b4ce-107">You can enable your users to automatically get signed-on to Wdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2b4ce-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="2b4ce-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="2b4ce-109">If you want to know more details about SaaS app integration with Azure AD, see.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="2b4ce-110">[What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="2b4ce-110">[What is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b4ce-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2b4ce-111">Prerequisites</span></span>

<span data-ttu-id="2b4ce-112">To configure Azure AD integration with Wdesk, you need the following items:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-112">To configure Azure AD integration with Wdesk, you need the following items:</span></span>

- <span data-ttu-id="2b4ce-113">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="2b4ce-113">An Azure AD subscription</span></span>
- <span data-ttu-id="2b4ce-114">A Wdesk single-sign on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="2b4ce-114">A Wdesk single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2b4ce-115">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2b4ce-116">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2b4ce-117">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2b4ce-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2b4ce-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2b4ce-119">Scenario description</span><span class="sxs-lookup"><span data-stu-id="2b4ce-119">Scenario description</span></span>
<span data-ttu-id="2b4ce-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2b4ce-121">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2b4ce-122">Adding Wdesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="2b4ce-122">Adding Wdesk from the gallery</span></span>
1. <span data-ttu-id="2b4ce-123">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b4ce-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wdesk-from-the-gallery"></a><span data-ttu-id="2b4ce-124">Adding Wdesk from the gallery</span><span class="sxs-lookup"><span data-stu-id="2b4ce-124">Adding Wdesk from the gallery</span></span>
<span data-ttu-id="2b4ce-125">To configure the integration of Wdesk into Azure AD, you need to add Wdesk from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-125">To configure the integration of Wdesk into Azure AD, you need to add Wdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="2b4ce-126">**To add Wdesk from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2b4ce-126">**To add Wdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="2b4ce-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="2b4ce-129">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="2b4ce-130">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-130">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="2b4ce-132">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="2b4ce-134">In the search box, type **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-134">In the search box, type **Wdesk**.</span></span>

    ![Creating an Azure AD test user](./media/wdesk-tutorial/tutorial_wdesk_search.png)

1. <span data-ttu-id="2b4ce-136">In the results panel, select **Wdesk**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-136">In the results panel, select **Wdesk**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/wdesk-tutorial/tutorial_wdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2b4ce-138">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b4ce-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2b4ce-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span><span class="sxs-lookup"><span data-stu-id="2b4ce-139">In this section, you configure and test Azure AD single sign-on with Wdesk based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="2b4ce-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Wdesk is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Wdesk is to a user in Azure AD.</span></span> <span data-ttu-id="2b4ce-141">In other words, a link relationship between an Azure AD user and the related user in Wdesk needs to be established.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-141">In other words, a link relationship between an Azure AD user and the related user in Wdesk needs to be established.</span></span>

<span data-ttu-id="2b4ce-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wdesk.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Wdesk.</span></span>

<span data-ttu-id="2b4ce-143">To configure and test Azure AD single sign-on with Wdesk, you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-143">To configure and test Azure AD single sign-on with Wdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="2b4ce-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="2b4ce-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="2b4ce-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - to have a counterpart of Britta Simon in Wdesk that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-146">**[Creating a Wdesk test user](#creating-a-wdesk-test-user)** - to have a counterpart of Britta Simon in Wdesk that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="2b4ce-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="2b4ce-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2b4ce-149">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b4ce-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2b4ce-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wdesk application.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wdesk application.</span></span>

<span data-ttu-id="2b4ce-151">**To configure Azure AD single sign-on with Wdesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2b4ce-151">**To configure Azure AD single sign-on with Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="2b4ce-152">In the Azure portal, on the **Wdesk** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-152">In the Azure portal, on the **Wdesk** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="2b4ce-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_wdesk_samlbase.png)

1. <span data-ttu-id="2b4ce-156">On the **Wdesk Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-156">On the **Wdesk Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_wdesk_url.png)

    <span data-ttu-id="2b4ce-158">a.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-158">a.</span></span> <span data-ttu-id="2b4ce-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="2b4ce-159">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/metadata/<instancename>`</span></span>

    <span data-ttu-id="2b4ce-160">b.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-160">b.</span></span> <span data-ttu-id="2b4ce-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="2b4ce-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/saml/sp/consumer/<instancename>`</span></span>

1. <span data-ttu-id="2b4ce-162">Check **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="2b4ce-163">If you wish to configure the application in **SP** initiated mode, perform the following step:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-163">If you wish to configure the application in **SP** initiated mode, perform the following step:</span></span>

    ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_wdesk_url1.png)

    <span data-ttu-id="2b4ce-165">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="2b4ce-165">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.wdesk.com/auth/login/saml/<instancename>`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="2b4ce-166">These values are not real.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-166">These values are not real.</span></span> <span data-ttu-id="2b4ce-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="2b4ce-168">You get these values from WDesk portal when you configure the SSO.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-168">You get these values from WDesk portal when you configure the SSO.</span></span> 
  
1. <span data-ttu-id="2b4ce-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_wdesk_certificate.png) 

1. <span data-ttu-id="2b4ce-171">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-171">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_general_400.png)
    
1. <span data-ttu-id="2b4ce-173">In a different web browser window, login to Wdesk as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-173">In a different web browser window, login to Wdesk as a Security Administrator.</span></span>

1. <span data-ttu-id="2b4ce-174">In the bottom left, click **Admin** and choose **Account Admin**:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-174">In the bottom left, click **Admin** and choose **Account Admin**:</span></span>
 
     ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

1. <span data-ttu-id="2b4ce-176">In Wdesk Admin, navigate to **Security**, then **SAML** > **SAML Settings**:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-176">In Wdesk Admin, navigate to **Security**, then **SAML** > **SAML Settings**:</span></span>

    ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_wdesk_ssoconfig2.png)

1. <span data-ttu-id="2b4ce-178">Under **General Settings**, check the **Enable SAML Single Sign On**:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-178">Under **General Settings**, check the **Enable SAML Single Sign On**:</span></span>

    ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_wdesk_ssoconfig3.png)

1. <span data-ttu-id="2b4ce-180">Under **Service Provider Details**, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-180">Under **Service Provider Details**, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_wdesk_ssoconfig4.png)

      <span data-ttu-id="2b4ce-182">a.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-182">a.</span></span> <span data-ttu-id="2b4ce-183">Copy the **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-183">Copy the **Login URL** and paste it in **Sign-on Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="2b4ce-184">b.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-184">b.</span></span> <span data-ttu-id="2b4ce-185">Copy the **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-185">Copy the **Metadata Url** and paste it in **Identifier** textbox on Azure portal.</span></span>
       
      <span data-ttu-id="2b4ce-186">c.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-186">c.</span></span> <span data-ttu-id="2b4ce-187">Copy the **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-187">Copy the **Consumer url** and paste it in **Reply Url** textbox on Azure portal.</span></span>
   
      <span data-ttu-id="2b4ce-188">d.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-188">d.</span></span> <span data-ttu-id="2b4ce-189">Click **Save** on Azure portal to save the changes.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-189">Click **Save** on Azure portal to save the changes.</span></span>      

1. <span data-ttu-id="2b4ce-190">Click **Configure IdP Settings** to open **Edit IdP Settings** dialog.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-190">Click **Configure IdP Settings** to open **Edit IdP Settings** dialog.</span></span> <span data-ttu-id="2b4ce-191">Click **Choose File** to locate the **Metadata.xml** file you saved from Azure portal, then upload it.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-191">Click **Choose File** to locate the **Metadata.xml** file you saved from Azure portal, then upload it.</span></span>
    
    ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_wdesk_ssoconfig5.png)
  
1. <span data-ttu-id="2b4ce-193">Click **Save changes**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-193">Click **Save changes**.</span></span>

    ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_wdesk_ssoconfigsavebutton.png)

> [!TIP]
> <span data-ttu-id="2b4ce-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="2b4ce-195">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="2b4ce-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-196">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="2b4ce-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2b4ce-197">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2b4ce-198">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2b4ce-198">Creating an Azure AD test user</span></span>
<span data-ttu-id="2b4ce-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-199">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="2b4ce-201">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2b4ce-201">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="2b4ce-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-202">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/wdesk-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="2b4ce-204">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-204">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/wdesk-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="2b4ce-206">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-206">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/wdesk-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="2b4ce-208">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-208">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/wdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2b4ce-210">a.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-210">a.</span></span> <span data-ttu-id="2b4ce-211">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-211">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2b4ce-212">b.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-212">b.</span></span> <span data-ttu-id="2b4ce-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-213">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2b4ce-214">c.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-214">c.</span></span> <span data-ttu-id="2b4ce-215">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-215">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="2b4ce-216">d.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-216">d.</span></span> <span data-ttu-id="2b4ce-217">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-217">Click **Create**.</span></span>
 
### <a name="creating-a-wdesk-test-user"></a><span data-ttu-id="2b4ce-218">Creating a Wdesk test user</span><span class="sxs-lookup"><span data-stu-id="2b4ce-218">Creating a Wdesk test user</span></span>

<span data-ttu-id="2b4ce-219">To enable Azure AD users to log in to Wdesk, they must be provisioned into Wdesk.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-219">To enable Azure AD users to log in to Wdesk, they must be provisioned into Wdesk.</span></span> <span data-ttu-id="2b4ce-220">In Wdesk, provisioning is a manual task.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-220">In Wdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="2b4ce-221">**To provision a user account, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2b4ce-221">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="2b4ce-222">Log in to Wdesk as a Security Administrator.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-222">Log in to Wdesk as a Security Administrator.</span></span>
1. <span data-ttu-id="2b4ce-223">Navigate to **Admin** > **Account Admin**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-223">Navigate to **Admin** > **Account Admin**.</span></span>

     ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_wdesk_ssoconfig1.png)

1. <span data-ttu-id="2b4ce-225">Click **Members** under **People**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-225">Click **Members** under **People**.</span></span>

1. <span data-ttu-id="2b4ce-226">Now click **Add Member** to open **Add Member** dialog box.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-226">Now click **Add Member** to open **Add Member** dialog box.</span></span> 
   
    ![Creating an Azure AD test user](./media/wdesk-tutorial/createuser1.png)  

1. <span data-ttu-id="2b4ce-228">In **User** text box, enter the username of user like **brittasimon@contoso.com** and click **Continue** button.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-228">In **User** text box, enter the username of user like **brittasimon@contoso.com** and click **Continue** button.</span></span>

    ![Creating an Azure AD test user](./media/wdesk-tutorial/createuser3.png)

1.  <span data-ttu-id="2b4ce-230">Enter the details as shown below:</span><span class="sxs-lookup"><span data-stu-id="2b4ce-230">Enter the details as shown below:</span></span>
  
    ![Creating an Azure AD test user](./media/wdesk-tutorial/createuser4.png)
 
    <span data-ttu-id="2b4ce-232">a.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-232">a.</span></span> <span data-ttu-id="2b4ce-233">In **E-mail** text box, enter the email of user like **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-233">In **E-mail** text box, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="2b4ce-234">b.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-234">b.</span></span> <span data-ttu-id="2b4ce-235">In **First Name** text box, enter the first name of user like **Britta**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-235">In **First Name** text box, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="2b4ce-236">c.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-236">c.</span></span> <span data-ttu-id="2b4ce-237">In **Last Name** text box, enter the last name of user like **Simon**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-237">In **Last Name** text box, enter the last name of user like **Simon**.</span></span>

1. <span data-ttu-id="2b4ce-238">Click **Save Member** button.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-238">Click **Save Member** button.</span></span>  

    ![Creating an Azure AD test user](./media/wdesk-tutorial/createuser5.png)

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="2b4ce-240">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="2b4ce-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="2b4ce-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wdesk.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wdesk.</span></span>

![Assign User][200] 

<span data-ttu-id="2b4ce-243">**To assign Britta Simon to Wdesk, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="2b4ce-243">**To assign Britta Simon to Wdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="2b4ce-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="2b4ce-246">In the applications list, select **Wdesk**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-246">In the applications list, select **Wdesk**.</span></span>

    ![Configure Single Sign-On](./media/wdesk-tutorial/tutorial_wdesk_app.png) 

1. <span data-ttu-id="2b4ce-248">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="2b4ce-250">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-250">Click **Add** button.</span></span> <span data-ttu-id="2b4ce-251">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="2b4ce-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="2b4ce-254">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-254">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="2b4ce-255">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2b4ce-256">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="2b4ce-256">Testing single sign-on</span></span>

<span data-ttu-id="2b4ce-257">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-257">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="2b4ce-258">When you click the Wdesk tile in the Access Panel, you should get automatically signed-on to your Wdesk application.</span><span class="sxs-lookup"><span data-stu-id="2b4ce-258">When you click the Wdesk tile in the Access Panel, you should get automatically signed-on to your Wdesk application.</span></span>
<span data-ttu-id="2b4ce-259">For more information about the Access Panel, see [introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2b4ce-259">For more information about the Access Panel, see [introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="2b4ce-260">Additional resources</span><span class="sxs-lookup"><span data-stu-id="2b4ce-260">Additional resources</span></span>

* [<span data-ttu-id="2b4ce-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2b4ce-261">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="2b4ce-262">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="2b4ce-262">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/wdesk-tutorial/tutorial_general_01.png
[2]: ./media/wdesk-tutorial/tutorial_general_02.png
[3]: ./media/wdesk-tutorial/tutorial_general_03.png
[4]: ./media/wdesk-tutorial/tutorial_general_04.png

[100]: ./media/wdesk-tutorial/tutorial_general_100.png

[200]: ./media/wdesk-tutorial/tutorial_general_200.png
[201]: ./media/wdesk-tutorial/tutorial_general_201.png
[202]: ./media/wdesk-tutorial/tutorial_general_202.png
[203]: ./media/wdesk-tutorial/tutorial_general_203.png

