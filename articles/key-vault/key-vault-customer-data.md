---
title: Azure Key Vault customer data features | Microsoft Docs
description: Learn about customer data in Key Vault
services: key-vault
documentationcenter: ''
author: barclayn
manager: mbaldwin
tags: azure-resource-manager
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: reference
ms.date: 05/22/2018
ms.author: barclayn
ms.openlocfilehash: 359648a843375477ea56ab791533208c11af9c81
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864706"
---
# <a name="azure-key-vault-customer-data-features"></a><span data-ttu-id="82537-103">Azure Key Vault customer data features</span><span class="sxs-lookup"><span data-stu-id="82537-103">Azure Key Vault customer data features</span></span>

<span data-ttu-id="82537-104">Azure Key Vault receives customer data during creation or update of vaults, keys, secrets, certificates, and managed storage accounts.</span><span class="sxs-lookup"><span data-stu-id="82537-104">Azure Key Vault receives customer data during creation or update of vaults, keys, secrets, certificates, and managed storage accounts.</span></span> <span data-ttu-id="82537-105">This Customer data is directly visible in the Azure portal and through the REST API.</span><span class="sxs-lookup"><span data-stu-id="82537-105">This Customer data is directly visible in the Azure portal and through the REST API.</span></span> <span data-ttu-id="82537-106">Customer data can be edited or deleted by updating or deleting the object that contains the data.</span><span class="sxs-lookup"><span data-stu-id="82537-106">Customer data can be edited or deleted by updating or deleting the object that contains the data.</span></span>

<span data-ttu-id="82537-107">System access logs are generated when a user or application accesses Key Vault.</span><span class="sxs-lookup"><span data-stu-id="82537-107">System access logs are generated when a user or application accesses Key Vault.</span></span> <span data-ttu-id="82537-108">Detailed access logs are available to customers using Azure Insights.</span><span class="sxs-lookup"><span data-stu-id="82537-108">Detailed access logs are available to customers using Azure Insights.</span></span>

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-intro-sentence.md)]

## <a name="identifying-customer-data"></a><span data-ttu-id="82537-109">Identifying customer data</span><span class="sxs-lookup"><span data-stu-id="82537-109">Identifying customer data</span></span>

<span data-ttu-id="82537-110">The following information identifies customer data within Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="82537-110">The following information identifies customer data within Azure Key Vault:</span></span>

- <span data-ttu-id="82537-111">Access policies for Azure Key Vault contain object-IDs representing users, groups, or applications</span><span class="sxs-lookup"><span data-stu-id="82537-111">Access policies for Azure Key Vault contain object-IDs representing users, groups, or applications</span></span>
- <span data-ttu-id="82537-112">Certificate subjects may include email addresses or other user or organizational identifiers</span><span class="sxs-lookup"><span data-stu-id="82537-112">Certificate subjects may include email addresses or other user or organizational identifiers</span></span>
- <span data-ttu-id="82537-113">Certificate contacts may contain user email addresses, names, or phone numbers</span><span class="sxs-lookup"><span data-stu-id="82537-113">Certificate contacts may contain user email addresses, names, or phone numbers</span></span>
- <span data-ttu-id="82537-114">Certificate issuers may contain email addresses, names, phone numbers, account credentials, and organizational details</span><span class="sxs-lookup"><span data-stu-id="82537-114">Certificate issuers may contain email addresses, names, phone numbers, account credentials, and organizational details</span></span>
- <span data-ttu-id="82537-115">Arbitrary tags can be applied to Objects in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="82537-115">Arbitrary tags can be applied to Objects in Azure Key Vault.</span></span> <span data-ttu-id="82537-116">These objects include vaults, keys, secrets, certificates, and storage accounts.</span><span class="sxs-lookup"><span data-stu-id="82537-116">These objects include vaults, keys, secrets, certificates, and storage accounts.</span></span> <span data-ttu-id="82537-117">The tags used may contain personal data</span><span class="sxs-lookup"><span data-stu-id="82537-117">The tags used may contain personal data</span></span>
- <span data-ttu-id="82537-118">Azure Key Vault access logs contain object-IDs, [UPNs](../active-directory/connect/active-directory-aadconnect-userprincipalname.md), and IP addresses for each REST API call</span><span class="sxs-lookup"><span data-stu-id="82537-118">Azure Key Vault access logs contain object-IDs, [UPNs](../active-directory/connect/active-directory-aadconnect-userprincipalname.md), and IP addresses for each REST API call</span></span>
- <span data-ttu-id="82537-119">Azure Key Vault diagnostic logs may contain object-IDs and IP addresses for REST API calls</span><span class="sxs-lookup"><span data-stu-id="82537-119">Azure Key Vault diagnostic logs may contain object-IDs and IP addresses for REST API calls</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="82537-120">Deleting customer data</span><span class="sxs-lookup"><span data-stu-id="82537-120">Deleting customer data</span></span>

<span data-ttu-id="82537-121">The same REST APIs, Portal experience, and SDKs used to create vaults, keys, secrets, certificates, and managed storage accounts, are also able to update and delete these objects.</span><span class="sxs-lookup"><span data-stu-id="82537-121">The same REST APIs, Portal experience, and SDKs used to create vaults, keys, secrets, certificates, and managed storage accounts, are also able to update and delete these objects.</span></span>

<span data-ttu-id="82537-122">Soft delete allows you to recover deleted data for 90 days after deletion.</span><span class="sxs-lookup"><span data-stu-id="82537-122">Soft delete allows you to recover deleted data for 90 days after deletion.</span></span> <span data-ttu-id="82537-123">When using soft delete, the data may be permanently deleted prior to the 90 days retention period expires by performing a purge operation.</span><span class="sxs-lookup"><span data-stu-id="82537-123">When using soft delete, the data may be permanently deleted prior to the 90 days retention period expires by performing a purge operation.</span></span> <span data-ttu-id="82537-124">If the vault or subscription has been configured to block purge operations, it is not possible to permanently delete data until the scheduled retention period has passed.</span><span class="sxs-lookup"><span data-stu-id="82537-124">If the vault or subscription has been configured to block purge operations, it is not possible to permanently delete data until the scheduled retention period has passed.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="82537-125">Exporting customer data</span><span class="sxs-lookup"><span data-stu-id="82537-125">Exporting customer data</span></span>

<span data-ttu-id="82537-126">The same REST APIs, portal experience, and SDKs that are used to create vaults, keys, secrets, certificates, and managed storage accounts  also allow you to view and export these objects.</span><span class="sxs-lookup"><span data-stu-id="82537-126">The same REST APIs, portal experience, and SDKs that are used to create vaults, keys, secrets, certificates, and managed storage accounts  also allow you to view and export these objects.</span></span>

<span data-ttu-id="82537-127">Azure Key Vault access logging is an optional feature that can be turned on to generate logs for each REST API call.</span><span class="sxs-lookup"><span data-stu-id="82537-127">Azure Key Vault access logging is an optional feature that can be turned on to generate logs for each REST API call.</span></span> <span data-ttu-id="82537-128">These logs will be transferred to a storage account in your subscription where you apply the retention policy that meets your organization's requirements.</span><span class="sxs-lookup"><span data-stu-id="82537-128">These logs will be transferred to a storage account in your subscription where you apply the retention policy that meets your organization's requirements.</span></span>

<span data-ttu-id="82537-129">Azure Key Vault diagnostic logs that contain personal data can be retrieved by making an export request in the User Privacy portal.</span><span class="sxs-lookup"><span data-stu-id="82537-129">Azure Key Vault diagnostic logs that contain personal data can be retrieved by making an export request in the User Privacy portal.</span></span> <span data-ttu-id="82537-130">This request must be made by the tenant administrator.</span><span class="sxs-lookup"><span data-stu-id="82537-130">This request must be made by the tenant administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82537-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="82537-131">Next steps</span></span>

- [<span data-ttu-id="82537-132">Azure Key Vault Logging</span><span class="sxs-lookup"><span data-stu-id="82537-132">Azure Key Vault Logging</span></span>](key-vault-logging.md)

- [<span data-ttu-id="82537-133">Azure Key Vault soft-delete overview</span><span class="sxs-lookup"><span data-stu-id="82537-133">Azure Key Vault soft-delete overview</span></span>](key-vault-soft-delete-cli.md)

- [<span data-ttu-id="82537-134">Azure Key Vault key operations</span><span class="sxs-lookup"><span data-stu-id="82537-134">Azure Key Vault key operations</span></span>](https://docs.microsoft.com/rest/api/keyvault/key-operations)

- [<span data-ttu-id="82537-135">Azure Key Vault secret operations</span><span class="sxs-lookup"><span data-stu-id="82537-135">Azure Key Vault secret operations</span></span>](https://docs.microsoft.com/rest/api/keyvault/secret-operations)

- [<span data-ttu-id="82537-136">Azure Key Vault certificates and policies</span><span class="sxs-lookup"><span data-stu-id="82537-136">Azure Key Vault certificates and policies</span></span>](https://docs.microsoft.com/rest/api/keyvault/certificates-and-policies)

- [<span data-ttu-id="82537-137">Azure Key Vault storage account operations</span><span class="sxs-lookup"><span data-stu-id="82537-137">Azure Key Vault storage account operations</span></span>](https://docs.microsoft.com/rest/api/keyvault/storage-account-key-operations)
