---
title: Use MSI in Azure Cloud Shell | Microsoft Docs
description: Authenticate code with MSI in Azure Cloud Shell
services: azure
documentationcenter: ''
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: ''
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2018
ms.author: juluk
ms.openlocfilehash: 99577faf7328dc773a9da5f7c1227aa63600aa0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856209"
---
# <a name="use-msi-in-azure-cloud-shell"></a><span data-ttu-id="19028-103">Use MSI in Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="19028-103">Use MSI in Azure Cloud Shell</span></span>

<span data-ttu-id="19028-104">Azure Cloud Shell supports authorization with Managed Service Identities (MSI).</span><span class="sxs-lookup"><span data-stu-id="19028-104">Azure Cloud Shell supports authorization with Managed Service Identities (MSI).</span></span> <span data-ttu-id="19028-105">Utilize this to retrieve access tokens to securely communicate with Azure services.</span><span class="sxs-lookup"><span data-stu-id="19028-105">Utilize this to retrieve access tokens to securely communicate with Azure services.</span></span>

## <a name="about-managed-service-identity-msi"></a><span data-ttu-id="19028-106">About Managed Service Identity (MSI)</span><span class="sxs-lookup"><span data-stu-id="19028-106">About Managed Service Identity (MSI)</span></span>
<span data-ttu-id="19028-107">A common challenge when building cloud applications is how to securely manage the credentials that need to be in your code for authenticating to cloud services.</span><span class="sxs-lookup"><span data-stu-id="19028-107">A common challenge when building cloud applications is how to securely manage the credentials that need to be in your code for authenticating to cloud services.</span></span> <span data-ttu-id="19028-108">In Cloud Shell you may need to authenticate retrieval from Key Vault for a credential that a script may need.</span><span class="sxs-lookup"><span data-stu-id="19028-108">In Cloud Shell you may need to authenticate retrieval from Key Vault for a credential that a script may need.</span></span>

<span data-ttu-id="19028-109">Managed Service Identity (MSI) makes solving this problem simpler by giving Azure services an automatically managed identity in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19028-109">Managed Service Identity (MSI) makes solving this problem simpler by giving Azure services an automatically managed identity in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="19028-110">You can use this identity to authenticate to any service that supports Azure AD authentication, including Key Vault, without having any credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="19028-110">You can use this identity to authenticate to any service that supports Azure AD authentication, including Key Vault, without having any credentials in your code.</span></span>

## <a name="acquire-access-token-in-cloud-shell"></a><span data-ttu-id="19028-111">Acquire access token in Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="19028-111">Acquire access token in Cloud Shell</span></span>

<span data-ttu-id="19028-112">Execute the following commands to set your MSI access token as an environment variable, `access_token`.</span><span class="sxs-lookup"><span data-stu-id="19028-112">Execute the following commands to set your MSI access token as an environment variable, `access_token`.</span></span>
```
response=$(curl http://localhost:50342/oauth2/token --data "resource=https://management.azure.com/" -H Metadata:true -s)
access_token=$(echo $response | python -c 'import sys, json; print (json.load(sys.stdin)["access_token"])')
echo The MSI access token is $access_token
```

## <a name="handling-token-expiration"></a><span data-ttu-id="19028-113">Handling token expiration</span><span class="sxs-lookup"><span data-stu-id="19028-113">Handling token expiration</span></span>

<span data-ttu-id="19028-114">The local MSI subsystem caches tokens.</span><span class="sxs-lookup"><span data-stu-id="19028-114">The local MSI subsystem caches tokens.</span></span> <span data-ttu-id="19028-115">Therefore, you can call it as often as you like, and an on-the-wire call to Azure AD results only if:</span><span class="sxs-lookup"><span data-stu-id="19028-115">Therefore, you can call it as often as you like, and an on-the-wire call to Azure AD results only if:</span></span>
- <span data-ttu-id="19028-116">a cache miss occurs due to no token in the cache</span><span class="sxs-lookup"><span data-stu-id="19028-116">a cache miss occurs due to no token in the cache</span></span>
- <span data-ttu-id="19028-117">the token is expired</span><span class="sxs-lookup"><span data-stu-id="19028-117">the token is expired</span></span>

<span data-ttu-id="19028-118">If you cache the token in your code, you should be prepared to handle scenarios where the resource indicates that the token is expired.</span><span class="sxs-lookup"><span data-stu-id="19028-118">If you cache the token in your code, you should be prepared to handle scenarios where the resource indicates that the token is expired.</span></span>

<span data-ttu-id="19028-119">To handle token errors, visit the [MSI page about curling MSI access tokens](https://docs.microsoft.com/azure/active-directory/managed-service-identity/how-to-use-vm-token#error-handling).</span><span class="sxs-lookup"><span data-stu-id="19028-119">To handle token errors, visit the [MSI page about curling MSI access tokens](https://docs.microsoft.com/azure/active-directory/managed-service-identity/how-to-use-vm-token#error-handling).</span></span>

## <a name="next-steps"></a><span data-ttu-id="19028-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="19028-120">Next steps</span></span>
[<span data-ttu-id="19028-121">Learn more about MSI</span><span class="sxs-lookup"><span data-stu-id="19028-121">Learn more about MSI</span></span>](https://docs.microsoft.com/azure/active-directory/managed-service-identity/overview)  
[<span data-ttu-id="19028-122">Acquiring access tokens from MSI VMs</span><span class="sxs-lookup"><span data-stu-id="19028-122">Acquiring access tokens from MSI VMs</span></span>](https://docs.microsoft.com/azure/active-directory/managed-service-identity/how-to-use-vm-token)
