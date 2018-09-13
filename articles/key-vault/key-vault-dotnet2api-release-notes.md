---
title: Key Vault .NET 2.x API Release Notes| Microsoft Docs
description: .NET developers will use this API to code for Azure Key Vault
services: key-vault
documentationcenter: ''
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 01/07/2017
ms.author: bruceper
ms.openlocfilehash: e3857174f97fe3143a59b0788ff409b9e1446b53
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555376"
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="c9caa-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span><span class="sxs-lookup"><span data-stu-id="c9caa-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="c9caa-104">The following notes and guidance are for developers working with the Azure Key Vault .NET / C# library.</span><span class="sxs-lookup"><span data-stu-id="c9caa-104">The following notes and guidance are for developers working with the Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="c9caa-105">In the change from the 1.0 version to the 2.0 version, a number of updates have been made that will require migration work in your code in order for you to benefit from the functional improvements and feature additions such as Key Vault certificates support.</span><span class="sxs-lookup"><span data-stu-id="c9caa-105">In the change from the 1.0 version to the 2.0 version, a number of updates have been made that will require migration work in your code in order for you to benefit from the functional improvements and feature additions such as Key Vault certificates support.</span></span>

<span data-ttu-id="c9caa-106">Key Vault certificates support provides for management of your x509 certificates and the following behaviors:</span><span class="sxs-lookup"><span data-stu-id="c9caa-106">Key Vault certificates support provides for management of your x509 certificates and the following behaviors:</span></span>  

* <span data-ttu-id="c9caa-107">Allows a certificate owner to create a certificate through a Key Vault creation process or through the import of an existing certificate.</span><span class="sxs-lookup"><span data-stu-id="c9caa-107">Allows a certificate owner to create a certificate through a Key Vault creation process or through the import of an existing certificate.</span></span> <span data-ttu-id="c9caa-108">This includes both self-signed and Certificate Authority generated certificates.</span><span class="sxs-lookup"><span data-stu-id="c9caa-108">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="c9caa-109">Allows a Key Vault certificate owner to implement secure storage and management of X509 certificates without interaction with private key material.</span><span class="sxs-lookup"><span data-stu-id="c9caa-109">Allows a Key Vault certificate owner to implement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="c9caa-110">Allows a certificate owner to create a policy that directs Key Vault to manage the life-cycle of a certificate.</span><span class="sxs-lookup"><span data-stu-id="c9caa-110">Allows a certificate owner to create a policy that directs Key Vault to manage the life-cycle of a certificate.</span></span>  
* <span data-ttu-id="c9caa-111">Allows certificate owners to provide contact information for notification about life-cycle events of expiration and renewal of certificate.</span><span class="sxs-lookup"><span data-stu-id="c9caa-111">Allows certificate owners to provide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="c9caa-112">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span><span class="sxs-lookup"><span data-stu-id="c9caa-112">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="c9caa-113">NOTE - Non-partnered providers/authorities are also allowed but, will not support the auto renewal feature.</span><span class="sxs-lookup"><span data-stu-id="c9caa-113">NOTE - Non-partnered providers/authorities are also allowed but, will not support the auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="c9caa-114">.NET support</span><span class="sxs-lookup"><span data-stu-id="c9caa-114">.NET support</span></span>
* <span data-ttu-id="c9caa-115">**.NET 4.0** is not supported by the 2.0 version of the Azure Key Vault .NET/C# library</span><span class="sxs-lookup"><span data-stu-id="c9caa-115">**.NET 4.0** is not supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="c9caa-116">**.NET Core** is supported by the 2.0 version of the Azure Key Vault .NET/C# library</span><span class="sxs-lookup"><span data-stu-id="c9caa-116">**.NET Core** is supported by the 2.0 version of the Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="c9caa-117">Namespaces</span><span class="sxs-lookup"><span data-stu-id="c9caa-117">Namespaces</span></span>
* <span data-ttu-id="c9caa-118">The namespace for **models** is changed from **Microsoft.Azure.KeyVault** to **Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="c9caa-118">The namespace for **models** is changed from **Microsoft.Azure.KeyVault** to **Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="c9caa-119">The **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span><span class="sxs-lookup"><span data-stu-id="c9caa-119">The **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="c9caa-120">The Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** to **Microsoft.Rest** and **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="c9caa-120">The Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** to **Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="c9caa-121">Type changes</span><span class="sxs-lookup"><span data-stu-id="c9caa-121">Type changes</span></span>
* <span data-ttu-id="c9caa-122">*Secret* changed to *SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="c9caa-122">*Secret* changed to *SecretBundle*</span></span>
* <span data-ttu-id="c9caa-123">*Dictionary* changed to *IDictionary*</span><span class="sxs-lookup"><span data-stu-id="c9caa-123">*Dictionary* changed to *IDictionary*</span></span>
* <span data-ttu-id="c9caa-124">*List<T>, string []* changed to *IList<T>*</span><span class="sxs-lookup"><span data-stu-id="c9caa-124">*List<T>, string []* changed to *IList<T>*</span></span>
* <span data-ttu-id="c9caa-125">*NextList* changed to  *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="c9caa-125">*NextList* changed to  *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="c9caa-126">Return types</span><span class="sxs-lookup"><span data-stu-id="c9caa-126">Return types</span></span>
* <span data-ttu-id="c9caa-127">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="c9caa-127">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="c9caa-128">The generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span><span class="sxs-lookup"><span data-stu-id="c9caa-128">The generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="c9caa-129">Before the method was wrapped and returning only the value.</span><span class="sxs-lookup"><span data-stu-id="c9caa-129">Before the method was wrapped and returning only the value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="c9caa-130">Exceptions</span><span class="sxs-lookup"><span data-stu-id="c9caa-130">Exceptions</span></span>
* <span data-ttu-id="c9caa-131">*KeyVaultClientException* is changed to *KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="c9caa-131">*KeyVaultClientException* is changed to *KeyVaultErrorException*</span></span>
* <span data-ttu-id="c9caa-132">The service error is changed from *exception.Error* to *exception.Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="c9caa-132">The service error is changed from *exception.Error* to *exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="c9caa-133">Removed additional info from the error message for **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="c9caa-133">Removed additional info from the error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="c9caa-134">Constructors</span><span class="sxs-lookup"><span data-stu-id="c9caa-134">Constructors</span></span>
* <span data-ttu-id="c9caa-135">Instead of accepting an *HttpClient* as a constructor argument, the constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span><span class="sxs-lookup"><span data-stu-id="c9caa-135">Instead of accepting an *HttpClient* as a constructor argument, the constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="c9caa-136">Downloaded packages</span><span class="sxs-lookup"><span data-stu-id="c9caa-136">Downloaded packages</span></span>
<span data-ttu-id="c9caa-137">When a client is processing a  dependency on Key Vault the following were downloaded</span><span class="sxs-lookup"><span data-stu-id="c9caa-137">When a client is processing a  dependency on Key Vault the following were downloaded</span></span>

#### <a name="previous-package-list"></a><span data-ttu-id="c9caa-138">Previous package list</span><span class="sxs-lookup"><span data-stu-id="c9caa-138">Previous package list</span></span>
* <span data-ttu-id="c9caa-139">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="c9caa-139">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="c9caa-140">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="c9caa-140">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="c9caa-141">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="c9caa-141">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="c9caa-142">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="c9caa-142">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="c9caa-143">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="c9caa-143">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="c9caa-144">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="c9caa-144">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="c9caa-145">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="c9caa-145">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="c9caa-146">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="c9caa-146">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

#### <a name="current-package-list"></a><span data-ttu-id="c9caa-147">Current package list</span><span class="sxs-lookup"><span data-stu-id="c9caa-147">Current package list</span></span>
* <span data-ttu-id="c9caa-148">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="c9caa-148">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="c9caa-149">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="c9caa-149">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="c9caa-150">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="c9caa-150">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="c9caa-151">Class changes</span><span class="sxs-lookup"><span data-stu-id="c9caa-151">Class changes</span></span>
* <span data-ttu-id="c9caa-152">**UnixEpoch** class has been removed</span><span class="sxs-lookup"><span data-stu-id="c9caa-152">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="c9caa-153">**Base64UrlConverter** class is renamed to **Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="c9caa-153">**Base64UrlConverter** class is renamed to **Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="c9caa-154">Other changes</span><span class="sxs-lookup"><span data-stu-id="c9caa-154">Other changes</span></span>
* <span data-ttu-id="c9caa-155">Support for the configuration of KV operation retry policy on transient failures has been added to this version of the API.</span><span class="sxs-lookup"><span data-stu-id="c9caa-155">Support for the configuration of KV operation retry policy on transient failures has been added to this version of the API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="c9caa-156">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="c9caa-156">Microsoft.Azure.Management.KeyVault NuGet</span></span>
* <span data-ttu-id="c9caa-157">For the operations that returned a *vault*, the return type was a class that contained a Vault property.</span><span class="sxs-lookup"><span data-stu-id="c9caa-157">For the operations that returned a *vault*, the return type was a class that contained a Vault property.</span></span> <span data-ttu-id="c9caa-158">The return type is now *Vault*.</span><span class="sxs-lookup"><span data-stu-id="c9caa-158">The return type is now *Vault*.</span></span>
* <span data-ttu-id="c9caa-159">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="c9caa-159">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="c9caa-160">Some of the return types changes apply to the control-plane as well.</span><span class="sxs-lookup"><span data-stu-id="c9caa-160">Some of the return types changes apply to the control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="c9caa-161">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="c9caa-161">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>
* <span data-ttu-id="c9caa-162">The package is broken up to **Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for the cryptography operations.</span><span class="sxs-lookup"><span data-stu-id="c9caa-162">The package is broken up to **Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for the cryptography operations.</span></span>

