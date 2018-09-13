---
title: 'Azure AD Connect: Device options | Microsoft Docs'
description: This document details device options available in Azure AD Connect
services: active-directory
documentationcenter: ''
author: billmath
manager: samueld
editor: billmath
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: e52f691c75d491897b06a4ebb492d87fda682e38
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864703"
---
#<a name="azure-ad-connect-device-options"></a><span data-ttu-id="b38bd-103">Azure AD Connect: Device options</span><span class="sxs-lookup"><span data-stu-id="b38bd-103">Azure AD Connect: Device options</span></span>

<span data-ttu-id="b38bd-104">The following documentation provides information about the various device options available in Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b38bd-104">The following documentation provides information about the various device options available in Azure AD Connect.</span></span> <span data-ttu-id="b38bd-105">You can use Azure AD Connect to configure the following two operations:</span><span class="sxs-lookup"><span data-stu-id="b38bd-105">You can use Azure AD Connect to configure the following two operations:</span></span> 
* <span data-ttu-id="b38bd-106">**Hybrid Azure AD join**: If your environment has an on-premises AD footprint and you also want benefit from the capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span><span class="sxs-lookup"><span data-stu-id="b38bd-106">**Hybrid Azure AD join**: If your environment has an on-premises AD footprint and you also want benefit from the capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="b38bd-107">These are devices that are both, joined to your on-premises Active Directory and your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b38bd-107">These are devices that are both, joined to your on-premises Active Directory and your Azure Active Directory.</span></span>
* <span data-ttu-id="b38bd-108">**Device writeback**: Device writeback is used to enable conditional access based on devices to AD FS (2012 R2 or higher) protected devices</span><span class="sxs-lookup"><span data-stu-id="b38bd-108">**Device writeback**: Device writeback is used to enable conditional access based on devices to AD FS (2012 R2 or higher) protected devices</span></span>

## <a name="configure-device-options-in-azure-ad-connect"></a><span data-ttu-id="b38bd-109">Configure device options in Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="b38bd-109">Configure device options in Azure AD Connect</span></span>

1.  <span data-ttu-id="b38bd-110">Run Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="b38bd-110">Run Azure AD Connect.</span></span> <span data-ttu-id="b38bd-111">In the **Additional tasks** page, select **Configure device options**.</span><span class="sxs-lookup"><span data-stu-id="b38bd-111">In the **Additional tasks** page, select **Configure device options**.</span></span>
    <span data-ttu-id="b38bd-112">![Configure device options](./media/active-directory-aadconnect-device-options/deviceoptions.png)</span><span class="sxs-lookup"><span data-stu-id="b38bd-112">![Configure device options](./media/active-directory-aadconnect-device-options/deviceoptions.png)</span></span> 

    <span data-ttu-id="b38bd-113">On clicking Next, an **Overview** page is displayed, which details the operations that can be performed.</span><span class="sxs-lookup"><span data-stu-id="b38bd-113">On clicking Next, an **Overview** page is displayed, which details the operations that can be performed.</span></span>
    <span data-ttu-id="b38bd-114">![Overview](./media/active-directory-aadconnect-device-options/deviceoverview.png)</span><span class="sxs-lookup"><span data-stu-id="b38bd-114">![Overview](./media/active-directory-aadconnect-device-options/deviceoverview.png)</span></span>

    >[!NOTE]
    > <span data-ttu-id="b38bd-115">The new Configure device options is available only in version 1.1.819.0 and newer.</span><span class="sxs-lookup"><span data-stu-id="b38bd-115">The new Configure device options is available only in version 1.1.819.0 and newer.</span></span>

2.  <span data-ttu-id="b38bd-116">After providing the credentials for Azure AD, you can chose the operation to be performed on the Device options page.</span><span class="sxs-lookup"><span data-stu-id="b38bd-116">After providing the credentials for Azure AD, you can chose the operation to be performed on the Device options page.</span></span>
    <span data-ttu-id="b38bd-117">![Device operations](./media/active-directory-aadconnect-device-options/deviceoptionsselection.png)</span><span class="sxs-lookup"><span data-stu-id="b38bd-117">![Device operations](./media/active-directory-aadconnect-device-options/deviceoptionsselection.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b38bd-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="b38bd-118">Next steps</span></span>

* [<span data-ttu-id="b38bd-119">Configure Hybrid Azure AD join</span><span class="sxs-lookup"><span data-stu-id="b38bd-119">Configure Hybrid Azure AD join</span></span>](../device-management-hybrid-azuread-joined-devices-setup.md)
* [<span data-ttu-id="b38bd-120">Configure / Disable device writeback</span><span class="sxs-lookup"><span data-stu-id="b38bd-120">Configure / Disable device writeback</span></span>](./active-directory-aadconnect-feature-device-writeback.md)

