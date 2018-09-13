---
title: Threat management in Azure Active Directory B2C | Microsoft Docs
description: Learn about detection and mitigation techniques for denial-of-service attacks and password attacks in Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 03/27/2016
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 1801fe9695aa15850d600300b957df2c7d7cd9ef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828880"
---
# <a name="azure-active-directory-b2c-threat-management"></a><span data-ttu-id="d7982-103">Azure Active Directory B2C: Threat management</span><span class="sxs-lookup"><span data-stu-id="d7982-103">Azure Active Directory B2C: Threat management</span></span>

<span data-ttu-id="d7982-104">Threat management includes planning for protection from attacks against your system and networks.</span><span class="sxs-lookup"><span data-stu-id="d7982-104">Threat management includes planning for protection from attacks against your system and networks.</span></span> <span data-ttu-id="d7982-105">Denial-of-service attacks might make resources unavailable to intended users.</span><span class="sxs-lookup"><span data-stu-id="d7982-105">Denial-of-service attacks might make resources unavailable to intended users.</span></span> <span data-ttu-id="d7982-106">Password attacks lead to unauthorized access to resources.</span><span class="sxs-lookup"><span data-stu-id="d7982-106">Password attacks lead to unauthorized access to resources.</span></span> <span data-ttu-id="d7982-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span><span class="sxs-lookup"><span data-stu-id="d7982-107">Azure Active Directory B2C (Azure AD B2C) has built-in features that can help you protect your data against these threats in multiple ways.</span></span>

## <a name="denial-of-service-attacks"></a><span data-ttu-id="d7982-108">Denial-of-service attacks</span><span class="sxs-lookup"><span data-stu-id="d7982-108">Denial-of-service attacks</span></span>

<span data-ttu-id="d7982-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits to protect underlying resources against denial-of-service attacks.</span><span class="sxs-lookup"><span data-stu-id="d7982-109">Azure AD B2C uses detection and mitigation techniques like SYN cookies, and rate and connection limits to protect underlying resources against denial-of-service attacks.</span></span>

## <a name="password-attacks"></a><span data-ttu-id="d7982-110">Password attacks</span><span class="sxs-lookup"><span data-stu-id="d7982-110">Password attacks</span></span>

<span data-ttu-id="d7982-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span><span class="sxs-lookup"><span data-stu-id="d7982-111">Azure AD B2C also has mitigation techniques in place for password attacks.</span></span> <span data-ttu-id="d7982-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span><span class="sxs-lookup"><span data-stu-id="d7982-112">Mitigation includes brute-force password attacks and dictionary password attacks.</span></span> <span data-ttu-id="d7982-113">Passwords that are set by users are required to be reasonably complex.</span><span class="sxs-lookup"><span data-stu-id="d7982-113">Passwords that are set by users are required to be reasonably complex.</span></span> <span data-ttu-id="d7982-114">By using various signals, Azure AD B2C analyzes the integrity of requests.</span><span class="sxs-lookup"><span data-stu-id="d7982-114">By using various signals, Azure AD B2C analyzes the integrity of requests.</span></span> <span data-ttu-id="d7982-115">Azure AD B2C is designed to intelligently differentiate intended users from hackers and botnets.</span><span class="sxs-lookup"><span data-stu-id="d7982-115">Azure AD B2C is designed to intelligently differentiate intended users from hackers and botnets.</span></span> <span data-ttu-id="d7982-116">Azure AD B2C provides a sophisticated strategy to lock accounts based on the passwords entered, in the likelihood of an attack.</span><span class="sxs-lookup"><span data-stu-id="d7982-116">Azure AD B2C provides a sophisticated strategy to lock accounts based on the passwords entered, in the likelihood of an attack.</span></span>

<span data-ttu-id="d7982-117">For more information, visit the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/default.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7982-117">For more information, visit the [Microsoft Trust Center](https://www.microsoft.com/trustcenter/default.aspx).</span></span>
