---
title: Manage protocols and ciphers in Azure API Management | Microsoft Docs
description: Learn how to manage protocols (TLS, SSL) and ciphers (DES) in Azure API Management.
services: api-management
documentationcenter: ''
author: mikebudzynski
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2018
ms.author: apimpm
ms.openlocfilehash: 454ba5c42694581bfa8fb1ec69ce97ac906b53d4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867192"
---
# <a name="manage-protocols-and-ciphers-in-azure-api-management"></a><span data-ttu-id="18f99-103">Manage protocols and ciphers in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="18f99-103">Manage protocols and ciphers in Azure API Management</span></span>

<span data-ttu-id="18f99-104">Azure API Management supports multiple versions of TLS protocol for both client and backend sides as well as the 3DES cipher.</span><span class="sxs-lookup"><span data-stu-id="18f99-104">Azure API Management supports multiple versions of TLS protocol for both client and backend sides as well as the 3DES cipher.</span></span>

<span data-ttu-id="18f99-105">This guide shows you how to manage protocols and ciphers configuration for an Azure API Management instance.</span><span class="sxs-lookup"><span data-stu-id="18f99-105">This guide shows you how to manage protocols and ciphers configuration for an Azure API Management instance.</span></span>

![Manage protocols and ciphers in APIM](./media/api-management-howto-manage-protocols-ciphers/api-management-protocols-ciphers.png)

## <a name="prerequisites"></a><span data-ttu-id="18f99-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="18f99-107">Prerequisites</span></span>

<span data-ttu-id="18f99-108">To follow the steps in this article, you must have:</span><span class="sxs-lookup"><span data-stu-id="18f99-108">To follow the steps in this article, you must have:</span></span>

* <span data-ttu-id="18f99-109">An API Management instance</span><span class="sxs-lookup"><span data-stu-id="18f99-109">An API Management instance</span></span>

## <a name="how-to-manage-tls-protocols-and-3des-cipher"></a><span data-ttu-id="18f99-110">How to manage TLS protocols and 3DES cipher</span><span class="sxs-lookup"><span data-stu-id="18f99-110">How to manage TLS protocols and 3DES cipher</span></span>

1. <span data-ttu-id="18f99-111">Navigate to your **API Management instance** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="18f99-111">Navigate to your **API Management instance** in the Azure portal.</span></span>
2. <span data-ttu-id="18f99-112">Select **SSL** from the menu.</span><span class="sxs-lookup"><span data-stu-id="18f99-112">Select **SSL** from the menu.</span></span>  
    <span data-ttu-id="18f99-113">![Manage protocols and ciphers in APIM - menu](./media/api-management-howto-manage-protocols-ciphers/api-management-menu.png)</span><span class="sxs-lookup"><span data-stu-id="18f99-113">![Manage protocols and ciphers in APIM - menu](./media/api-management-howto-manage-protocols-ciphers/api-management-menu.png)</span></span>
3. <span data-ttu-id="18f99-114">Enable or disable desired protocols or ciphers.</span><span class="sxs-lookup"><span data-stu-id="18f99-114">Enable or disable desired protocols or ciphers.</span></span>
4. <span data-ttu-id="18f99-115">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="18f99-115">Click **Save**.</span></span> <span data-ttu-id="18f99-116">Changes will be applied within an hour.</span><span class="sxs-lookup"><span data-stu-id="18f99-116">Changes will be applied within an hour.</span></span>  
    <span data-ttu-id="18f99-117">![Manage protocols and ciphers in APIM - save](./media/api-management-howto-manage-protocols-ciphers/api-management-protocols-ciphers-save.png)</span><span class="sxs-lookup"><span data-stu-id="18f99-117">![Manage protocols and ciphers in APIM - save](./media/api-management-howto-manage-protocols-ciphers/api-management-protocols-ciphers-save.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="18f99-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="18f99-118">Next steps</span></span>

* <span data-ttu-id="18f99-119">Learn more about [TLS (Transport Layer Security)](https://docs.microsoft.com/en-us/dotnet/framework/network-programming/tls).</span><span class="sxs-lookup"><span data-stu-id="18f99-119">Learn more about [TLS (Transport Layer Security)](https://docs.microsoft.com/en-us/dotnet/framework/network-programming/tls).</span></span>
* <span data-ttu-id="18f99-120">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span><span class="sxs-lookup"><span data-stu-id="18f99-120">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>