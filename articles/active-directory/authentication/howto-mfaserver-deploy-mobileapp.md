---
title: Azure MFA Server Mobile App Web Service | Microsoft Docs
description: Configure MFA server to send push notifications to users with the Microsoft Authenticator App.
services: multi-factor-authentication
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: michmcla
ms.openlocfilehash: d31cf6569f642d2c7b61abe25148f5cfb199f0a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871647"
---
# <a name="enable-mobile-app-authentication-with-azure-multi-factor-authentication-server"></a><span data-ttu-id="6ea6a-103">Enable mobile app authentication with Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="6ea6a-103">Enable mobile app authentication with Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="6ea6a-104">The Microsoft Authenticator app offers an additional out-of-band verification option.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-104">The Microsoft Authenticator app offers an additional out-of-band verification option.</span></span> <span data-ttu-id="6ea6a-105">Instead of placing an automated phone call or SMS to the user during login, Azure Multi-Factor Authentication pushes a notification to the Microsoft Authenticator app on the user’s smartphone or tablet.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-105">Instead of placing an automated phone call or SMS to the user during login, Azure Multi-Factor Authentication pushes a notification to the Microsoft Authenticator app on the user’s smartphone or tablet.</span></span> <span data-ttu-id="6ea6a-106">The user simply taps **Verify** (or enters a PIN and taps “Authenticate”) in the app to complete their sign-in.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-106">The user simply taps **Verify** (or enters a PIN and taps “Authenticate”) in the app to complete their sign-in.</span></span>

<span data-ttu-id="6ea6a-107">Using a mobile app for two-step verification is preferred when phone reception is unreliable.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-107">Using a mobile app for two-step verification is preferred when phone reception is unreliable.</span></span> <span data-ttu-id="6ea6a-108">If you use the app as an OATH token generator, it doesn't require any network or internet connection.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-108">If you use the app as an OATH token generator, it doesn't require any network or internet connection.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ea6a-109">If you have installed Azure Multi-Factor Authentication Server v8.x or higher, most of the steps below are not required.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-109">If you have installed Azure Multi-Factor Authentication Server v8.x or higher, most of the steps below are not required.</span></span> <span data-ttu-id="6ea6a-110">Mobile app authentication can be set up by following the steps under [Configure the mobile app](#configure-the-mobile-app-settings-in-the-azure-multi-factor-authentication-server).</span><span class="sxs-lookup"><span data-stu-id="6ea6a-110">Mobile app authentication can be set up by following the steps under [Configure the mobile app](#configure-the-mobile-app-settings-in-the-azure-multi-factor-authentication-server).</span></span>

## <a name="requirements"></a><span data-ttu-id="6ea6a-111">Requirements</span><span class="sxs-lookup"><span data-stu-id="6ea6a-111">Requirements</span></span>

<span data-ttu-id="6ea6a-112">To use the Microsoft Authenticator app, you must be running Azure Multi-Factor Authentication Server v8.x or higher</span><span class="sxs-lookup"><span data-stu-id="6ea6a-112">To use the Microsoft Authenticator app, you must be running Azure Multi-Factor Authentication Server v8.x or higher</span></span>

## <a name="configure-the-mobile-app-settings-in-the-azure-multi-factor-authentication-server"></a><span data-ttu-id="6ea6a-113">Configure the mobile app settings in the Azure Multi-Factor Authentication Server</span><span class="sxs-lookup"><span data-stu-id="6ea6a-113">Configure the mobile app settings in the Azure Multi-Factor Authentication Server</span></span>

1. <span data-ttu-id="6ea6a-114">In the Multi-Factor Authentication Server console, click the User Portal icon.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-114">In the Multi-Factor Authentication Server console, click the User Portal icon.</span></span> <span data-ttu-id="6ea6a-115">If users are allowed to control their authentication methods, check **Mobile App** on the Settings tab, under **Allow users to select method**.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-115">If users are allowed to control their authentication methods, check **Mobile App** on the Settings tab, under **Allow users to select method**.</span></span> <span data-ttu-id="6ea6a-116">Without this feature enabled, end users are required to contact your Help Desk to complete activation for the Mobile App.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-116">Without this feature enabled, end users are required to contact your Help Desk to complete activation for the Mobile App.</span></span>
2. <span data-ttu-id="6ea6a-117">Check the **Allow users to activate Mobile App** box.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-117">Check the **Allow users to activate Mobile App** box.</span></span>
3. <span data-ttu-id="6ea6a-118">Check the **Allow User Enrollment** box.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-118">Check the **Allow User Enrollment** box.</span></span>
4. <span data-ttu-id="6ea6a-119">Click the **Mobile App** icon.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-119">Click the **Mobile App** icon.</span></span>
5. <span data-ttu-id="6ea6a-120">Populate the **Account name** field with the company or organization name to display in the mobile application for this account.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-120">Populate the **Account name** field with the company or organization name to display in the mobile application for this account.</span></span>
   <span data-ttu-id="6ea6a-121">![MFA Server configuration Mobile App settings](./media/howto-mfaserver-deploy-mobileapp/mobile.png)</span><span class="sxs-lookup"><span data-stu-id="6ea6a-121">![MFA Server configuration Mobile App settings](./media/howto-mfaserver-deploy-mobileapp/mobile.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ea6a-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="6ea6a-122">Next steps</span></span>

- <span data-ttu-id="6ea6a-123">[Advanced scenarios with Azure Multi-Factor Authentication and third-party VPNs](howto-mfaserver-nps-vpn.md).</span><span class="sxs-lookup"><span data-stu-id="6ea6a-123">[Advanced scenarios with Azure Multi-Factor Authentication and third-party VPNs](howto-mfaserver-nps-vpn.md).</span></span>
