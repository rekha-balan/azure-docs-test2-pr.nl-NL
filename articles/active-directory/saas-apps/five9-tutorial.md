---
title: 'Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents) | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Five9 Plus Adapter (CTI, Contact Center Agents).
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 88dc82ab-be0b-4017-8335-c47d00775d7b
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: 8ee04008b62867c8eba68b1525cf50edec881cbc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965981"
---
# <a name="tutorial-azure-active-directory-integration-with-five9-plus-adapter-cti-contact-center-agents"></a><span data-ttu-id="61a7c-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="61a7c-103">Tutorial: Azure Active Directory integration with Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>

<span data-ttu-id="61a7c-104">In this tutorial, you learn how to integrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="61a7c-104">In this tutorial, you learn how to integrate Five9 Plus Adapter (CTI, Contact Center Agents) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="61a7c-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="61a7c-105">Integrating Five9 Plus Adapter (CTI, Contact Center Agents) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="61a7c-106">You can control in Azure AD who has access to Five9 Plus Adapter (CTI, Contact Center Agents)</span><span class="sxs-lookup"><span data-stu-id="61a7c-106">You can control in Azure AD who has access to Five9 Plus Adapter (CTI, Contact Center Agents)</span></span>
- <span data-ttu-id="61a7c-107">You can enable your users to automatically get signed-on to Five9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span><span class="sxs-lookup"><span data-stu-id="61a7c-107">You can enable your users to automatically get signed-on to Five9 Plus Adapter (CTI, Contact Center Agents) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="61a7c-108">You can manage your accounts in one central location - the Azure portal</span><span class="sxs-lookup"><span data-stu-id="61a7c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="61a7c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span><span class="sxs-lookup"><span data-stu-id="61a7c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](../manage-apps/what-is-single-sign-on.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="61a7c-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="61a7c-110">Prerequisites</span></span>

<span data-ttu-id="61a7c-111">To configure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need the following items:</span><span class="sxs-lookup"><span data-stu-id="61a7c-111">To configure Azure AD integration with Five9 Plus Adapter (CTI, Contact Center Agents), you need the following items:</span></span>

- <span data-ttu-id="61a7c-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="61a7c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="61a7c-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span><span class="sxs-lookup"><span data-stu-id="61a7c-113">A Five9 Plus Adapter (CTI, Contact Center Agents) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="61a7c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span><span class="sxs-lookup"><span data-stu-id="61a7c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="61a7c-115">To test the steps in this tutorial, you should follow these recommendations:</span><span class="sxs-lookup"><span data-stu-id="61a7c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="61a7c-116">Do not use your production environment, unless it is necessary.</span><span class="sxs-lookup"><span data-stu-id="61a7c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="61a7c-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="61a7c-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="61a7c-118">Scenario description</span><span class="sxs-lookup"><span data-stu-id="61a7c-118">Scenario description</span></span>
<span data-ttu-id="61a7c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span><span class="sxs-lookup"><span data-stu-id="61a7c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="61a7c-120">The scenario outlined in this tutorial consists of two main building blocks:</span><span class="sxs-lookup"><span data-stu-id="61a7c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="61a7c-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span><span class="sxs-lookup"><span data-stu-id="61a7c-121">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span></span>
1. <span data-ttu-id="61a7c-122">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61a7c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-five9-plus-adapter-cti-contact-center-agents-from-the-gallery"></a><span data-ttu-id="61a7c-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span><span class="sxs-lookup"><span data-stu-id="61a7c-123">Adding Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery</span></span>
<span data-ttu-id="61a7c-124">To configure the integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need to add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery to your list of managed SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="61a7c-124">To configure the integration of Five9 Plus Adapter (CTI, Contact Center Agents) into Azure AD, you need to add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="61a7c-125">**To add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61a7c-125">**To add Five9 Plus Adapter (CTI, Contact Center Agents) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="61a7c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="61a7c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

1. <span data-ttu-id="61a7c-128">Navigate to **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="61a7c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="61a7c-129">Then go to **All applications**.</span><span class="sxs-lookup"><span data-stu-id="61a7c-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
1. <span data-ttu-id="61a7c-131">To add new application, click **New application** button on the top of dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Applications][3]

1. <span data-ttu-id="61a7c-133">In the search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span><span class="sxs-lookup"><span data-stu-id="61a7c-133">In the search box, type **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Creating an Azure AD test user](./media/five9-tutorial/tutorial_five9_search.png)

1. <span data-ttu-id="61a7c-135">In the results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button to add the application.</span><span class="sxs-lookup"><span data-stu-id="61a7c-135">In the results panel, select **Five9 Plus Adapter (CTI, Contact Center Agents)**, and then click **Add** button to add the application.</span></span>

    ![Creating an Azure AD test user](./media/five9-tutorial/tutorial_five9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="61a7c-137">Configuring and testing Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61a7c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="61a7c-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span><span class="sxs-lookup"><span data-stu-id="61a7c-138">In this section, you configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="61a7c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is to a user in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="61a7c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Five9 Plus Adapter (CTI, Contact Center Agents) is to a user in Azure AD.</span></span> <span data-ttu-id="61a7c-140">In other words, a link relationship between an Azure AD user and the related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs to be established.</span><span class="sxs-lookup"><span data-stu-id="61a7c-140">In other words, a link relationship between an Azure AD user and the related user in Five9 Plus Adapter (CTI, Contact Center Agents) needs to be established.</span></span>

<span data-ttu-id="61a7c-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span><span class="sxs-lookup"><span data-stu-id="61a7c-141">In Five9 Plus Adapter (CTI, Contact Center Agents), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="61a7c-142">To configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need to complete the following building blocks:</span><span class="sxs-lookup"><span data-stu-id="61a7c-142">To configure and test Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="61a7c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span><span class="sxs-lookup"><span data-stu-id="61a7c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
1. <span data-ttu-id="61a7c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61a7c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
1. <span data-ttu-id="61a7c-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - to have a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked to the Azure AD representation of user.</span><span class="sxs-lookup"><span data-stu-id="61a7c-145">**[Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user](#creating-a-five9-plus-adapter-cti-contact-center-agents-test-user)** - to have a counterpart of Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents) that is linked to the Azure AD representation of user.</span></span>
1. <span data-ttu-id="61a7c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61a7c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
1. <span data-ttu-id="61a7c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span><span class="sxs-lookup"><span data-stu-id="61a7c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="61a7c-148">Configuring Azure AD single sign-on</span><span class="sxs-lookup"><span data-stu-id="61a7c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="61a7c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span><span class="sxs-lookup"><span data-stu-id="61a7c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>

<span data-ttu-id="61a7c-150">**To configure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61a7c-150">**To configure Azure AD single sign-on with Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span></span>

1. <span data-ttu-id="61a7c-151">In the Azure portal, on the **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span><span class="sxs-lookup"><span data-stu-id="61a7c-151">In the Azure portal, on the **Five9 Plus Adapter (CTI, Contact Center Agents)** application integration page, click **Single sign-on**.</span></span>

    ![Configure Single Sign-On][4]

1. <span data-ttu-id="61a7c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61a7c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Configure Single Sign-On](./media/five9-tutorial/tutorial_five9_samlbase.png)

1. <span data-ttu-id="61a7c-155">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61a7c-155">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Domain and URLs** section, perform the following steps:</span></span>

    ![Configure Single Sign-On](./media/five9-tutorial/tutorial_five9_url.png)
    
    <span data-ttu-id="61a7c-157">a.</span><span class="sxs-lookup"><span data-stu-id="61a7c-157">a.</span></span> <span data-ttu-id="61a7c-158">In the **Identifier** textbox, type a URL using the following patterns:</span><span class="sxs-lookup"><span data-stu-id="61a7c-158">In the **Identifier** textbox, type a URL using the following patterns:</span></span>

    |    <span data-ttu-id="61a7c-159">Environment</span><span class="sxs-lookup"><span data-stu-id="61a7c-159">Environment</span></span>      |       <span data-ttu-id="61a7c-160">URL</span><span class="sxs-lookup"><span data-stu-id="61a7c-160">URL</span></span>      |
    | :-- | :-- |
    | <span data-ttu-id="61a7c-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span><span class="sxs-lookup"><span data-stu-id="61a7c-161">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/msdc` |
    | <span data-ttu-id="61a7c-162">For “Five9 Plus Adapter for Zendesk”</span><span class="sxs-lookup"><span data-stu-id="61a7c-162">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/zd` |
    | <span data-ttu-id="61a7c-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span><span class="sxs-lookup"><span data-stu-id="61a7c-163">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/metadata/alias/adt` |

    <span data-ttu-id="61a7c-164">b.</span><span class="sxs-lookup"><span data-stu-id="61a7c-164">b.</span></span> <span data-ttu-id="61a7c-165">In the **Reply URL** textbox, type a URL using the following pattern:</span><span class="sxs-lookup"><span data-stu-id="61a7c-165">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>

    |      <span data-ttu-id="61a7c-166">Environment</span><span class="sxs-lookup"><span data-stu-id="61a7c-166">Environment</span></span>     |      <span data-ttu-id="61a7c-167">URL</span><span class="sxs-lookup"><span data-stu-id="61a7c-167">URL</span></span>      |
    | :--                  | :--           |
    | <span data-ttu-id="61a7c-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span><span class="sxs-lookup"><span data-stu-id="61a7c-168">For “Five9 Plus Adapter for Microsoft Dynamics CRM”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/msdc` |
    | <span data-ttu-id="61a7c-169">For “Five9 Plus Adapter for Zendesk”</span><span class="sxs-lookup"><span data-stu-id="61a7c-169">For “Five9 Plus Adapter for Zendesk”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/zd` |
    | <span data-ttu-id="61a7c-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span><span class="sxs-lookup"><span data-stu-id="61a7c-170">For “Five9 Plus Adapter for Agent Desktop Toolkit”</span></span> | `https://app.five9.com/appsvcs/saml/SSO/alias/adt` |

1. <span data-ttu-id="61a7c-171">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span><span class="sxs-lookup"><span data-stu-id="61a7c-171">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Configure Single Sign-On](./media/five9-tutorial/tutorial_five9_certificate.png) 

1. <span data-ttu-id="61a7c-173">Click **Save** button.</span><span class="sxs-lookup"><span data-stu-id="61a7c-173">Click **Save** button.</span></span>

    ![Configure Single Sign-On](./media/five9-tutorial/tutorial_general_400.png)

1. <span data-ttu-id="61a7c-175">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** to open **Configure sign-on** window.</span><span class="sxs-lookup"><span data-stu-id="61a7c-175">On the **Five9 Plus Adapter (CTI, Contact Center Agents) Configuration** section, click **Configure Five9 Plus Adapter (CTI, Contact Center Agents)** to open **Configure sign-on** window.</span></span> <span data-ttu-id="61a7c-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span><span class="sxs-lookup"><span data-stu-id="61a7c-176">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Configure Single Sign-On](./media/five9-tutorial/tutorial_five9_configure.png) 

1. <span data-ttu-id="61a7c-178">To configure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span><span class="sxs-lookup"><span data-stu-id="61a7c-178">To configure single sign-on on **Five9 Plus Adapter (CTI, Contact Center Agents)** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact).</span></span> <span data-ttu-id="61a7c-179">Also additionally, for configuring SSO further please follow the below steps according to the adapter:</span><span class="sxs-lookup"><span data-stu-id="61a7c-179">Also additionally, for configuring SSO further please follow the below steps according to the adapter:</span></span>

    <span data-ttu-id="61a7c-180">a.</span><span class="sxs-lookup"><span data-stu-id="61a7c-180">a.</span></span> <span data-ttu-id="61a7c-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="61a7c-181">“Five9 Plus Adapter for Agent Desktop Toolkit” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/agent-desktop-toolkit/plus-agent-desktop-toolkit-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="61a7c-182">b.</span><span class="sxs-lookup"><span data-stu-id="61a7c-182">b.</span></span> <span data-ttu-id="61a7c-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="61a7c-183">“Five9 Plus Adapter for Microsoft Dynamics CRM” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/microsoft/microsoft-administrators-guide.pdf)</span></span>
    
    <span data-ttu-id="61a7c-184">c.</span><span class="sxs-lookup"><span data-stu-id="61a7c-184">c.</span></span> <span data-ttu-id="61a7c-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span><span class="sxs-lookup"><span data-stu-id="61a7c-185">“Five9 Plus Adapter for Zendesk” Admin Guide: [http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf](http://webapps.five9.com/assets/files/for_customers/documentation/integrations/zendesk/zendesk-plus-administrators-guide.pdf)</span></span>


> [!TIP]
> <span data-ttu-id="61a7c-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span><span class="sxs-lookup"><span data-stu-id="61a7c-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="61a7c-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span><span class="sxs-lookup"><span data-stu-id="61a7c-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="61a7c-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="61a7c-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="61a7c-189">Creating an Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="61a7c-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="61a7c-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="61a7c-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Create Azure AD User][100]

<span data-ttu-id="61a7c-192">**To create a test user in Azure AD, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61a7c-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="61a7c-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span><span class="sxs-lookup"><span data-stu-id="61a7c-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Creating an Azure AD test user](./media/five9-tutorial/create_aaduser_01.png) 

1. <span data-ttu-id="61a7c-195">To display the list of users, go to **Users and groups** and click **All users**.</span><span class="sxs-lookup"><span data-stu-id="61a7c-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Creating an Azure AD test user](./media/five9-tutorial/create_aaduser_02.png) 

1. <span data-ttu-id="61a7c-197">To open the **User** dialog, click **Add** on the top of the dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7c-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Creating an Azure AD test user](./media/five9-tutorial/create_aaduser_03.png) 

1. <span data-ttu-id="61a7c-199">On the **User** dialog page, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="61a7c-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Creating an Azure AD test user](./media/five9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="61a7c-201">a.</span><span class="sxs-lookup"><span data-stu-id="61a7c-201">a.</span></span> <span data-ttu-id="61a7c-202">In the **Name** textbox, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="61a7c-202">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="61a7c-203">b.</span><span class="sxs-lookup"><span data-stu-id="61a7c-203">b.</span></span> <span data-ttu-id="61a7c-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="61a7c-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="61a7c-205">c.</span><span class="sxs-lookup"><span data-stu-id="61a7c-205">c.</span></span> <span data-ttu-id="61a7c-206">Select **Show Password** and write down the value of the **Password**.</span><span class="sxs-lookup"><span data-stu-id="61a7c-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="61a7c-207">d.</span><span class="sxs-lookup"><span data-stu-id="61a7c-207">d.</span></span> <span data-ttu-id="61a7c-208">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="61a7c-208">Click **Create**.</span></span>
 
### <a name="creating-a-five9-plus-adapter-cti-contact-center-agents-test-user"></a><span data-ttu-id="61a7c-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span><span class="sxs-lookup"><span data-stu-id="61a7c-209">Creating a Five9 Plus Adapter (CTI, Contact Center Agents) test user</span></span>

<span data-ttu-id="61a7c-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="61a7c-210">In this section, you create a user called Britta Simon in Five9 Plus Adapter (CTI, Contact Center Agents).</span></span> <span data-ttu-id="61a7c-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add the users in the Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span><span class="sxs-lookup"><span data-stu-id="61a7c-211">Work with [Five9 Plus Adapter (CTI, Contact Center Agents) support team](https://www.five9.com/about/contact) to add the users in the Five9 Plus Adapter (CTI, Contact Center Agents) platform.</span></span> <span data-ttu-id="61a7c-212">Users must be created and activated before you use single sign-on.</span><span class="sxs-lookup"><span data-stu-id="61a7c-212">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="61a7c-213">Assigning the Azure AD test user</span><span class="sxs-lookup"><span data-stu-id="61a7c-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="61a7c-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Five9 Plus Adapter (CTI, Contact Center Agents).</span><span class="sxs-lookup"><span data-stu-id="61a7c-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Five9 Plus Adapter (CTI, Contact Center Agents).</span></span>

![Assign User][200] 

<span data-ttu-id="61a7c-216">**To assign Britta Simon to Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="61a7c-216">**To assign Britta Simon to Five9 Plus Adapter (CTI, Contact Center Agents), perform the following steps:**</span></span>

1. <span data-ttu-id="61a7c-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span><span class="sxs-lookup"><span data-stu-id="61a7c-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Assign User][201] 

1. <span data-ttu-id="61a7c-219">In the applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span><span class="sxs-lookup"><span data-stu-id="61a7c-219">In the applications list, select **Five9 Plus Adapter (CTI, Contact Center Agents)**.</span></span>

    ![Configure Single Sign-On](./media/five9-tutorial/tutorial_five9_app.png) 

1. <span data-ttu-id="61a7c-221">In the menu on the left, click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="61a7c-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Assign User][202] 

1. <span data-ttu-id="61a7c-223">Click **Add** button.</span><span class="sxs-lookup"><span data-stu-id="61a7c-223">Click **Add** button.</span></span> <span data-ttu-id="61a7c-224">Then select **Users and groups** on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7c-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Assign User][203]

1. <span data-ttu-id="61a7c-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span><span class="sxs-lookup"><span data-stu-id="61a7c-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

1. <span data-ttu-id="61a7c-227">Click **Select** button on **Users and groups** dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7c-227">Click **Select** button on **Users and groups** dialog.</span></span>

1. <span data-ttu-id="61a7c-228">Click **Assign** button on **Add Assignment** dialog.</span><span class="sxs-lookup"><span data-stu-id="61a7c-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="61a7c-229">Testing single sign-on</span><span class="sxs-lookup"><span data-stu-id="61a7c-229">Testing single sign-on</span></span>

<span data-ttu-id="61a7c-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="61a7c-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="61a7c-231">When you click the Five9 Plus Adapter (CTI, Contact Center Agents) tile in the Access Panel, you should get automatically signed-on to your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span><span class="sxs-lookup"><span data-stu-id="61a7c-231">When you click the Five9 Plus Adapter (CTI, Contact Center Agents) tile in the Access Panel, you should get automatically signed-on to your Five9 Plus Adapter (CTI, Contact Center Agents) application.</span></span>
<span data-ttu-id="61a7c-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="61a7c-232">For more information about the Access Panel, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="61a7c-233">Additional resources</span><span class="sxs-lookup"><span data-stu-id="61a7c-233">Additional resources</span></span>

* [<span data-ttu-id="61a7c-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="61a7c-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](tutorial-list.md)
* [<span data-ttu-id="61a7c-235">What is application access and single sign-on with Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="61a7c-235">What is application access and single sign-on with Azure Active Directory?</span></span>](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/five9-tutorial/tutorial_general_01.png
[2]: ./media/five9-tutorial/tutorial_general_02.png
[3]: ./media/five9-tutorial/tutorial_general_03.png
[4]: ./media/five9-tutorial/tutorial_general_04.png

[100]: ./media/five9-tutorial/tutorial_general_100.png

[200]: ./media/five9-tutorial/tutorial_general_200.png
[201]: ./media/five9-tutorial/tutorial_general_201.png
[202]: ./media/five9-tutorial/tutorial_general_202.png
[203]: ./media/five9-tutorial/tutorial_general_203.png

