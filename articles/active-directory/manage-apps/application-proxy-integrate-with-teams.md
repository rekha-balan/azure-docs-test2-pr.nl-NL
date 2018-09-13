---
title: Access Azure AD App Proxy apps in Teams | Microsoft Docs
description: Use Azure AD Application Proxy to access your on-premises application through Microsoft Teams.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/05/2017
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 1269dfb3aec33e781601a1d885004ddf80127160
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870742"
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a><span data-ttu-id="101f5-103">Access your on-premises applications through Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="101f5-103">Access your on-premises applications through Microsoft Teams</span></span>

<span data-ttu-id="101f5-104">Azure Active Directory Application Proxy gives you single sign-on to on-premises applications no matter where you are.</span><span class="sxs-lookup"><span data-stu-id="101f5-104">Azure Active Directory Application Proxy gives you single sign-on to on-premises applications no matter where you are.</span></span> <span data-ttu-id="101f5-105">Microsoft Teams streamlines your collaborative efforts in one place.</span><span class="sxs-lookup"><span data-stu-id="101f5-105">Microsoft Teams streamlines your collaborative efforts in one place.</span></span> <span data-ttu-id="101f5-106">Integrating the two together means that your users can be productive with their teammates in any situation.</span><span class="sxs-lookup"><span data-stu-id="101f5-106">Integrating the two together means that your users can be productive with their teammates in any situation.</span></span> 

<span data-ttu-id="101f5-107">Your users can add cloud apps to their Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what about the SharePoint sites or planning tool that are hosted on-premises?</span><span class="sxs-lookup"><span data-stu-id="101f5-107">Your users can add cloud apps to their Teams channels [using tabs](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), but what about the SharePoint sites or planning tool that are hosted on-premises?</span></span> <span data-ttu-id="101f5-108">Application Proxy is the solution.</span><span class="sxs-lookup"><span data-stu-id="101f5-108">Application Proxy is the solution.</span></span> <span data-ttu-id="101f5-109">They can add apps published through Application Proxy to their channels using the same external URLs they always use to access their apps remotely.</span><span class="sxs-lookup"><span data-stu-id="101f5-109">They can add apps published through Application Proxy to their channels using the same external URLs they always use to access their apps remotely.</span></span> <span data-ttu-id="101f5-110">And because Application Proxy authenticates through Azure Active Directory, your users get a single sign-on experience.</span><span class="sxs-lookup"><span data-stu-id="101f5-110">And because Application Proxy authenticates through Azure Active Directory, your users get a single sign-on experience.</span></span>


## <a name="install-the-application-proxy-connector-and-publish-your-app"></a><span data-ttu-id="101f5-111">Install the Application Proxy connector and publish your app</span><span class="sxs-lookup"><span data-stu-id="101f5-111">Install the Application Proxy connector and publish your app</span></span>

<span data-ttu-id="101f5-112">If you haven't already, [configure Application Proxy for your tenant and install the connector](application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="101f5-112">If you haven't already, [configure Application Proxy for your tenant and install the connector](application-proxy-enable.md).</span></span> <span data-ttu-id="101f5-113">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span><span class="sxs-lookup"><span data-stu-id="101f5-113">Then, [publish your on-premises application](application-proxy-publish-azure-portal.md) for remote access.</span></span> <span data-ttu-id="101f5-114">When you're publishing the app, make note of the external URL because it's used to add the app to Teams.</span><span class="sxs-lookup"><span data-stu-id="101f5-114">When you're publishing the app, make note of the external URL because it's used to add the app to Teams.</span></span>

<span data-ttu-id="101f5-115">If you already have your apps published but don't remember their external URLs, look them up in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="101f5-115">If you already have your apps published but don't remember their external URLs, look them up in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="101f5-116">Sign in, then navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span><span class="sxs-lookup"><span data-stu-id="101f5-116">Sign in, then navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** > select your app > **Application proxy**.</span></span>

## <a name="add-your-app-to-teams"></a><span data-ttu-id="101f5-117">Add your app to Teams</span><span class="sxs-lookup"><span data-stu-id="101f5-117">Add your app to Teams</span></span>

<span data-ttu-id="101f5-118">Once you publish the app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels, and then the app is available for everyone in the team to use.</span><span class="sxs-lookup"><span data-stu-id="101f5-118">Once you publish the app through Application Proxy, let your users know that they can add it as a tab directly in their Teams channels, and then the app is available for everyone in the team to use.</span></span> <span data-ttu-id="101f5-119">Have them follow these three steps:</span><span class="sxs-lookup"><span data-stu-id="101f5-119">Have them follow these three steps:</span></span>

1. <span data-ttu-id="101f5-120">Navigate to the Teams channel where you want to add this app and select **+** to add a tab.</span><span class="sxs-lookup"><span data-stu-id="101f5-120">Navigate to the Teams channel where you want to add this app and select **+** to add a tab.</span></span>

   ![Select Add a tab](./media/application-proxy-integrate-with-teams/add-tab.png)

2. <span data-ttu-id="101f5-122">Select **Website** from the tab options.</span><span class="sxs-lookup"><span data-stu-id="101f5-122">Select **Website** from the tab options.</span></span>

   ![Add a website](./media/application-proxy-integrate-with-teams/website.png)

3. <span data-ttu-id="101f5-124">Give the tab a name and set the URL to the Application Proxy external URL.</span><span class="sxs-lookup"><span data-stu-id="101f5-124">Give the tab a name and set the URL to the Application Proxy external URL.</span></span> 

   ![Configure tab name and URL](./media/application-proxy-integrate-with-teams/tab-name-url.png)

<span data-ttu-id="101f5-126">Once one member of a team adds the tab, it shows up for everyone in the channel.</span><span class="sxs-lookup"><span data-stu-id="101f5-126">Once one member of a team adds the tab, it shows up for everyone in the channel.</span></span> <span data-ttu-id="101f5-127">Any users who have access to the app get single sign-on access with the credentials they use for Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="101f5-127">Any users who have access to the app get single sign-on access with the credentials they use for Microsoft Teams.</span></span> <span data-ttu-id="101f5-128">Any users who don't have access to the app can see the tab in Teams, but are blocked until you give them permissions to the on-premises app and the Azure portal published version of the app.</span><span class="sxs-lookup"><span data-stu-id="101f5-128">Any users who don't have access to the app can see the tab in Teams, but are blocked until you give them permissions to the on-premises app and the Azure portal published version of the app.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="101f5-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="101f5-129">Next steps</span></span>

- <span data-ttu-id="101f5-130">Learn how to [publish on-premises SharePoint sites](application-proxy-integrate-with-sharepoint-server.md) with Application Proxy.</span><span class="sxs-lookup"><span data-stu-id="101f5-130">Learn how to [publish on-premises SharePoint sites](application-proxy-integrate-with-sharepoint-server.md) with Application Proxy.</span></span>
- <span data-ttu-id="101f5-131">Configure your apps to use [custom domains](application-proxy-configure-custom-domain.md) for their external URL.</span><span class="sxs-lookup"><span data-stu-id="101f5-131">Configure your apps to use [custom domains](application-proxy-configure-custom-domain.md) for their external URL.</span></span> 
