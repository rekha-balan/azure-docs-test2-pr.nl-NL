---
title: Integer claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C  | Microsoft Docs
description: Integer claims transformation examples for the Identity Experience Framework Schema of Azure Active Directory B2C.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: reference
ms.date: 09/10/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 988e25b6a5ef3f99ae7df9076a40e06b403bb029
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857412"
---
# <a name="integer-claims-transformations"></a><span data-ttu-id="712ff-103">Integer claims transformations</span><span class="sxs-lookup"><span data-stu-id="712ff-103">Integer claims transformations</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="712ff-104">This article provides examples for using the integer claims transformations of the Identity Experience Framework schema in Azure Active Directory (Azure AD) B2C.</span><span class="sxs-lookup"><span data-stu-id="712ff-104">This article provides examples for using the integer claims transformations of the Identity Experience Framework schema in Azure Active Directory (Azure AD) B2C.</span></span> <span data-ttu-id="712ff-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span><span class="sxs-lookup"><span data-stu-id="712ff-105">For more information, see [ClaimsTransformations](claimstransformations.md).</span></span>

## <a name="convertnumbertostringclaim"></a><span data-ttu-id="712ff-106">ConvertNumberToStringClaim</span><span class="sxs-lookup"><span data-stu-id="712ff-106">ConvertNumberToStringClaim</span></span> 

<span data-ttu-id="712ff-107">Converts a long data type into a string data type.</span><span class="sxs-lookup"><span data-stu-id="712ff-107">Converts a long data type into a string data type.</span></span>

| <span data-ttu-id="712ff-108">Item</span><span class="sxs-lookup"><span data-stu-id="712ff-108">Item</span></span> | <span data-ttu-id="712ff-109">TransformationClaimType</span><span class="sxs-lookup"><span data-stu-id="712ff-109">TransformationClaimType</span></span> | <span data-ttu-id="712ff-110">Data Type</span><span class="sxs-lookup"><span data-stu-id="712ff-110">Data Type</span></span> | <span data-ttu-id="712ff-111">Notes</span><span class="sxs-lookup"><span data-stu-id="712ff-111">Notes</span></span> |
| ---- | ----------------------- | --------- | ----- |
| <span data-ttu-id="712ff-112">InputClaim</span><span class="sxs-lookup"><span data-stu-id="712ff-112">InputClaim</span></span> | <span data-ttu-id="712ff-113">inputClaim</span><span class="sxs-lookup"><span data-stu-id="712ff-113">inputClaim</span></span> | <span data-ttu-id="712ff-114">long</span><span class="sxs-lookup"><span data-stu-id="712ff-114">long</span></span> | <span data-ttu-id="712ff-115">The ClaimType to convert to a string.</span><span class="sxs-lookup"><span data-stu-id="712ff-115">The ClaimType to convert to a string.</span></span> |
| <span data-ttu-id="712ff-116">OutputClaim</span><span class="sxs-lookup"><span data-stu-id="712ff-116">OutputClaim</span></span> | <span data-ttu-id="712ff-117">outputClaim</span><span class="sxs-lookup"><span data-stu-id="712ff-117">outputClaim</span></span> | <span data-ttu-id="712ff-118">string</span><span class="sxs-lookup"><span data-stu-id="712ff-118">string</span></span> | <span data-ttu-id="712ff-119">The ClaimType that is produced after this ClaimsTransformation has been invoked.</span><span class="sxs-lookup"><span data-stu-id="712ff-119">The ClaimType that is produced after this ClaimsTransformation has been invoked.</span></span> |

<span data-ttu-id="712ff-120">In this example, the `numericUserId` claim with a value type of long is converted to a `UserId` claim with a value type of string.</span><span class="sxs-lookup"><span data-stu-id="712ff-120">In this example, the `numericUserId` claim with a value type of long is converted to a `UserId` claim with a value type of string.</span></span>

```XML
<ClaimsTransformation Id="CreateUserId" TransformationMethod="ConvertNumberToStringClaim">
  <InputClaims>
    <InputClaim ClaimTypeReferenceId="numericUserId" TransformationClaimType="inputClaim" />
  </InputClaims>
  <OutputClaims>
    <OutputClaim ClaimTypeReferenceId="UserId" TransformationClaimType="outputClaim" />
  </OutputClaims>
</ClaimsTransformation>
```

### <a name="example"></a><span data-ttu-id="712ff-121">Example</span><span class="sxs-lookup"><span data-stu-id="712ff-121">Example</span></span>

- <span data-ttu-id="712ff-122">Input claims:</span><span class="sxs-lookup"><span data-stu-id="712ff-122">Input claims:</span></span>
    - <span data-ttu-id="712ff-123">**inputClaim**: 12334 (long)</span><span class="sxs-lookup"><span data-stu-id="712ff-123">**inputClaim**: 12334 (long)</span></span>
- <span data-ttu-id="712ff-124">Output claims:</span><span class="sxs-lookup"><span data-stu-id="712ff-124">Output claims:</span></span> 
    - <span data-ttu-id="712ff-125">**outputClaim**: "12334" (string)</span><span class="sxs-lookup"><span data-stu-id="712ff-125">**outputClaim**: "12334" (string)</span></span>

