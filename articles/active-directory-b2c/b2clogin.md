---
title: Using b2clogin.com | Microsoft Docs
description: Learn about using b2clogin.com instead of login.microsoftonline.com.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/29/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 6ad0a5d59b28bf48742c9e1be89b51d2301dd582
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870753"
---
# <a name="using-b2clogincom"></a><span data-ttu-id="dcb21-103">Using b2clogin.com</span><span class="sxs-lookup"><span data-stu-id="dcb21-103">Using b2clogin.com</span></span>

>[!IMPORTANT]
><span data-ttu-id="dcb21-104">This feature is public preview</span><span class="sxs-lookup"><span data-stu-id="dcb21-104">This feature is public preview</span></span> 
>

<span data-ttu-id="dcb21-105">You now have the option to use the Azure AD B2C service with `<YourTenantName>.b2clogin.com` instead of using `login.microsoftonline.com`.</span><span class="sxs-lookup"><span data-stu-id="dcb21-105">You now have the option to use the Azure AD B2C service with `<YourTenantName>.b2clogin.com` instead of using `login.microsoftonline.com`.</span></span>  <span data-ttu-id="dcb21-106">This has many benefits:</span><span class="sxs-lookup"><span data-stu-id="dcb21-106">This has many benefits:</span></span>
* <span data-ttu-id="dcb21-107">You no longer share the same cookie header size limit with the other Microsoft products.</span><span class="sxs-lookup"><span data-stu-id="dcb21-107">You no longer share the same cookie header size limit with the other Microsoft products.</span></span>
* <span data-ttu-id="dcb21-108">You can remove all references to Microsoft in your URL (you can replace `<YourTenantName>.onmicrosoft.com` with your tenant ID).</span><span class="sxs-lookup"><span data-stu-id="dcb21-108">You can remove all references to Microsoft in your URL (you can replace `<YourTenantName>.onmicrosoft.com` with your tenant ID).</span></span> <span data-ttu-id="dcb21-109">For example: `https://<tenantname>.b2clogin.com/tfp/<tenantID>/<policyname>/v2.0/.well-known/openid-configuration`.</span><span class="sxs-lookup"><span data-stu-id="dcb21-109">For example: `https://<tenantname>.b2clogin.com/tfp/<tenantID>/<policyname>/v2.0/.well-known/openid-configuration`.</span></span>

 <span data-ttu-id="dcb21-110">In order to take advantage of b2clogin.com, you need to set some of the following:</span><span class="sxs-lookup"><span data-stu-id="dcb21-110">In order to take advantage of b2clogin.com, you need to set some of the following:</span></span>

1. <span data-ttu-id="dcb21-111">For your **Run now endpoint** make sure you are using `<YourTenantName>.b2clogin.com` instead of using `login.microsoftonline.com`.</span><span class="sxs-lookup"><span data-stu-id="dcb21-111">For your **Run now endpoint** make sure you are using `<YourTenantName>.b2clogin.com` instead of using `login.microsoftonline.com`.</span></span>
2. <span data-ttu-id="dcb21-112">If you are using MSAL, you need to set `validateauthority=false`.</span><span class="sxs-lookup"><span data-stu-id="dcb21-112">If you are using MSAL, you need to set `validateauthority=false`.</span></span>  <span data-ttu-id="dcb21-113">This is because the token issuer becomes`<YourTenantName>.b2clogin.com`.</span><span class="sxs-lookup"><span data-stu-id="dcb21-113">This is because the token issuer becomes`<YourTenantName>.b2clogin.com`.</span></span>
