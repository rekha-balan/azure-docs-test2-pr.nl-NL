---
title: Monitor and manage certificate creation
description: Scenarios demonstrating a range of options for creating, monitoring, and interacting with the certificate creation process with Key Vault.
services: key-vault
documentationcenter: ''
author: bryanla
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 0d0995aa-b60d-4811-be12-ba0a45390197
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/09/2018
ms.author: bryanla
ms.openlocfilehash: 0e24bd56123279a24a72b9b52d8cb51e2a3a5eae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868822"
---
# <a name="monitor-and-manage-certificate-creation"></a><span data-ttu-id="5e8b5-103">Monitor and manage certificate creation</span><span class="sxs-lookup"><span data-stu-id="5e8b5-103">Monitor and manage certificate creation</span></span>
<span data-ttu-id="5e8b5-104">Applies To: Azure</span><span class="sxs-lookup"><span data-stu-id="5e8b5-104">Applies To: Azure</span></span>  

<span data-ttu-id="5e8b5-105">The following</span><span class="sxs-lookup"><span data-stu-id="5e8b5-105">The following</span></span> 

<span data-ttu-id="5e8b5-106">The scenarios / operations outlined in this article are:</span><span class="sxs-lookup"><span data-stu-id="5e8b5-106">The scenarios / operations outlined in this article are:</span></span>

- <span data-ttu-id="5e8b5-107">Request a KV Certificate with a supported issuer</span><span class="sxs-lookup"><span data-stu-id="5e8b5-107">Request a KV Certificate with a supported issuer</span></span>
- <span data-ttu-id="5e8b5-108">Get pending request - request status is "inProgress"</span><span class="sxs-lookup"><span data-stu-id="5e8b5-108">Get pending request - request status is "inProgress"</span></span>
- <span data-ttu-id="5e8b5-109">Get pending request - request status is "complete"</span><span class="sxs-lookup"><span data-stu-id="5e8b5-109">Get pending request - request status is "complete"</span></span>
- <span data-ttu-id="5e8b5-110">Get pending request - pending request status is "canceled" or "failed"</span><span class="sxs-lookup"><span data-stu-id="5e8b5-110">Get pending request - pending request status is "canceled" or "failed"</span></span>
- <span data-ttu-id="5e8b5-111">Get pending request - pending request status is "deleted" or "overwritten"</span><span class="sxs-lookup"><span data-stu-id="5e8b5-111">Get pending request - pending request status is "deleted" or "overwritten"</span></span>
- <span data-ttu-id="5e8b5-112">Create (or Import) when pending request exists - status is "inProgress"</span><span class="sxs-lookup"><span data-stu-id="5e8b5-112">Create (or Import) when pending request exists - status is "inProgress"</span></span>
- <span data-ttu-id="5e8b5-113">Merge when pending request is created with an issuer (DigiCert, for example)</span><span class="sxs-lookup"><span data-stu-id="5e8b5-113">Merge when pending request is created with an issuer (DigiCert, for example)</span></span>
- <span data-ttu-id="5e8b5-114">Request a cancellation while the pending request status is "inProgress"</span><span class="sxs-lookup"><span data-stu-id="5e8b5-114">Request a cancellation while the pending request status is "inProgress"</span></span>
- <span data-ttu-id="5e8b5-115">Delete a pending request object</span><span class="sxs-lookup"><span data-stu-id="5e8b5-115">Delete a pending request object</span></span>
- <span data-ttu-id="5e8b5-116">Create a KV certificate manually</span><span class="sxs-lookup"><span data-stu-id="5e8b5-116">Create a KV certificate manually</span></span>
- <span data-ttu-id="5e8b5-117">Merge when a pending request is created - manual certificate creation</span><span class="sxs-lookup"><span data-stu-id="5e8b5-117">Merge when a pending request is created - manual certificate creation</span></span>

## <a name="request-a-kv-certificate-with-a-supported-issuer"></a><span data-ttu-id="5e8b5-118">Request a KV Certificate with a supported issuer</span><span class="sxs-lookup"><span data-stu-id="5e8b5-118">Request a KV Certificate with a supported issuer</span></span> 

|<span data-ttu-id="5e8b5-119">Method</span><span class="sxs-lookup"><span data-stu-id="5e8b5-119">Method</span></span>|<span data-ttu-id="5e8b5-120">Request URI</span><span class="sxs-lookup"><span data-stu-id="5e8b5-120">Request URI</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="5e8b5-121">POST</span><span class="sxs-lookup"><span data-stu-id="5e8b5-121">POST</span></span>|`https://mykeyvault.vault.azure.net/certificates/mycert1/create?api-version={api-version}`|  

<span data-ttu-id="5e8b5-122">The following examples require an object named "mydigicert" to already be available in your key vault with the issuer provider as DigiCert.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-122">The following examples require an object named "mydigicert" to already be available in your key vault with the issuer provider as DigiCert.</span></span> <span data-ttu-id="5e8b5-123">The certificate issuer is an entity represented in Azure Key Vault (KV) as a CertificateIssuer resource.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-123">The certificate issuer is an entity represented in Azure Key Vault (KV) as a CertificateIssuer resource.</span></span> <span data-ttu-id="5e8b5-124">It is used to provide information about the source of a KV certificate; issuer name, provider, credentials, and other administrative details.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-124">It is used to provide information about the source of a KV certificate; issuer name, provider, credentials, and other administrative details.</span></span>  

### <a name="request"></a><span data-ttu-id="5e8b5-125">Request</span><span class="sxs-lookup"><span data-stu-id="5e8b5-125">Request</span></span>  

```json
{  
  "policy": {  
    "x509_props": {  
      "subject": "CN=MyCertSubject1"  
    },  
  "issuer": {  
       "name": "mydigicert",  
    "cty": "OV-SSL",  
    }  
  }  
}  

```  

### <a name="response"></a><span data-ttu-id="5e8b5-126">Response</span><span class="sxs-lookup"><span data-stu-id="5e8b5-126">Response</span></span>  

```  
StatusCode: 202, ReasonPhrase: 'Accepted'  
Location: “https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"  
{  
  "id": “https://mykeyvault.vault.azure.net/certificates/mycert1/pending",  
  "issuer": {  
    "name": "mydigicert"  
  },  
  "csr": "MIICq......DD5Lp5cqXg==",  
  "cancellation_requested": false,  
  "status": "InProgress",  
  "status_details": "Pending certificate created. Certificate request is in progress. This may take some time based on the issuer provider. Please check again later",  
  "request_id": "a76827a18b63421c917da80f28e9913d"  
}  

```  

## <a name="get-pending-request---request-status-is-inprogress"></a><span data-ttu-id="5e8b5-127">Get pending request - request status is "inProgress"</span><span class="sxs-lookup"><span data-stu-id="5e8b5-127">Get pending request - request status is "inProgress"</span></span>

|<span data-ttu-id="5e8b5-128">Method</span><span class="sxs-lookup"><span data-stu-id="5e8b5-128">Method</span></span>|<span data-ttu-id="5e8b5-129">Request URI</span><span class="sxs-lookup"><span data-stu-id="5e8b5-129">Request URI</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="5e8b5-130">GET</span><span class="sxs-lookup"><span data-stu-id="5e8b5-130">GET</span></span>|`https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}`|  

### <a name="request"></a><span data-ttu-id="5e8b5-131">Request</span><span class="sxs-lookup"><span data-stu-id="5e8b5-131">Request</span></span>  
 <span data-ttu-id="5e8b5-132">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"`</span><span class="sxs-lookup"><span data-stu-id="5e8b5-132">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"`</span></span>  

 <span data-ttu-id="5e8b5-133">OR</span><span class="sxs-lookup"><span data-stu-id="5e8b5-133">OR</span></span>  

 <span data-ttu-id="5e8b5-134">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}"`</span><span class="sxs-lookup"><span data-stu-id="5e8b5-134">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}"`</span></span>  

> [!NOTE]
>  <span data-ttu-id="5e8b5-135">If *request_id* is specified in the query, it acts like a filter.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-135">If *request_id* is specified in the query, it acts like a filter.</span></span> <span data-ttu-id="5e8b5-136">If the *request_id* in the query and in the pending object are different, an http status code of 404 is returned.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-136">If the *request_id* in the query and in the pending object are different, an http status code of 404 is returned.</span></span>  

### <a name="response"></a><span data-ttu-id="5e8b5-137">Response</span><span class="sxs-lookup"><span data-stu-id="5e8b5-137">Response</span></span>  

```  
StatusCode: 200, ReasonPhrase: 'OK'  
{  
  "id": “https://mykeyvault.vault.azure.net/certificates/mycert1/pending",  
  "issuer": {  
    "name": "{issuer-name}"  
  },  
  "csr": "MIICq......DD5Lp5cqXg==",  
  "cancellation_requested": false,  
  "status": "inProgress",  
  "status_details": "…",  
  "request_id": "a76827a18b63421c917da80f28e9913d"  
}  

```  

## <a name="get-pending-request---request-status-is-complete"></a><span data-ttu-id="5e8b5-138">Get pending request - request status is "complete"</span><span class="sxs-lookup"><span data-stu-id="5e8b5-138">Get pending request - request status is "complete"</span></span>

### <a name="request"></a><span data-ttu-id="5e8b5-139">Request</span><span class="sxs-lookup"><span data-stu-id="5e8b5-139">Request</span></span>  

|<span data-ttu-id="5e8b5-140">Method</span><span class="sxs-lookup"><span data-stu-id="5e8b5-140">Method</span></span>|<span data-ttu-id="5e8b5-141">Request URI</span><span class="sxs-lookup"><span data-stu-id="5e8b5-141">Request URI</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="5e8b5-142">GET</span><span class="sxs-lookup"><span data-stu-id="5e8b5-142">GET</span></span>|`https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}`|  

 <span data-ttu-id="5e8b5-143">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"`</span><span class="sxs-lookup"><span data-stu-id="5e8b5-143">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"`</span></span>  

 <span data-ttu-id="5e8b5-144">OR</span><span class="sxs-lookup"><span data-stu-id="5e8b5-144">OR</span></span>  

 <span data-ttu-id="5e8b5-145">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}"`</span><span class="sxs-lookup"><span data-stu-id="5e8b5-145">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}"`</span></span>  

### <a name="response"></a><span data-ttu-id="5e8b5-146">Response</span><span class="sxs-lookup"><span data-stu-id="5e8b5-146">Response</span></span>  

```  
StatusCode: 200, ReasonPhrase: 'OK'  
{  
  "id": “https://mykeyvault.vault.azure.net/certificates/mycert1/pending",  
  "issuer": {  
    "name": "{issuer-name}"  
  },  
  "csr": "MIICq......DD5Lp5cqXg==",  
  "cancellation_requested": false,  
  "status": "completed",  
  "request_id": "a76827a18b63421c917da80f28e9913d",  
   "target": “https://mykeyvault.vault.azure.net/certificates/mycert1?api-version={api-version}"  
}  

```  

## <a name="get-pending-request---pending-request-status-is-canceled-or-failed"></a><span data-ttu-id="5e8b5-147">Get pending request - pending request status is "canceled" or "failed"</span><span class="sxs-lookup"><span data-stu-id="5e8b5-147">Get pending request - pending request status is "canceled" or "failed"</span></span>  

### <a name="request"></a><span data-ttu-id="5e8b5-148">Request</span><span class="sxs-lookup"><span data-stu-id="5e8b5-148">Request</span></span>  

|<span data-ttu-id="5e8b5-149">Method</span><span class="sxs-lookup"><span data-stu-id="5e8b5-149">Method</span></span>|<span data-ttu-id="5e8b5-150">Request URI</span><span class="sxs-lookup"><span data-stu-id="5e8b5-150">Request URI</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="5e8b5-151">GET</span><span class="sxs-lookup"><span data-stu-id="5e8b5-151">GET</span></span>|`https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}`|  

 <span data-ttu-id="5e8b5-152">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"`</span><span class="sxs-lookup"><span data-stu-id="5e8b5-152">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"`</span></span>  

 <span data-ttu-id="5e8b5-153">OR</span><span class="sxs-lookup"><span data-stu-id="5e8b5-153">OR</span></span>  

 <span data-ttu-id="5e8b5-154">GET  `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}"`</span><span class="sxs-lookup"><span data-stu-id="5e8b5-154">GET  `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}"`</span></span>  

### <a name="response"></a><span data-ttu-id="5e8b5-155">Response</span><span class="sxs-lookup"><span data-stu-id="5e8b5-155">Response</span></span>  

```  
StatusCode: 200, ReasonPhrase: 'OK'  
{  
  "id": “https://mykeyvault.vault.azure.net/certificates/mycert1/pending",  
  "issuer": {  
    "name": "{issuer-name}"  
  },  
  "csr": "MIICq......DD5Lp5cqXg==",  
  "cancellation_requested": false,  
  "status": "failed",  
  "status_details": "",  
  "request_id": "a76827a18b63421c917da80f28e9913d",  
   "error":  
    {  
        "code": "<errorcode>",    
        "message": "<message>"  
    }  
}  

```  

> [!NOTE]
> <span data-ttu-id="5e8b5-156">The value of the *errorcode* can be "Certificate issuer error" or "Request rejected" based on issuer or user error respectively.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-156">The value of the *errorcode* can be "Certificate issuer error" or "Request rejected" based on issuer or user error respectively.</span></span>  

## <a name="get-pending-request---pending-request-status-is-deleted-or-overwritten"></a><span data-ttu-id="5e8b5-157">Get pending request - pending request status is "deleted" or "overwritten"</span><span class="sxs-lookup"><span data-stu-id="5e8b5-157">Get pending request - pending request status is "deleted" or "overwritten"</span></span>  
 <span data-ttu-id="5e8b5-158">A pending object can be deleted or overwritten by a create/import operation when its status is not "inProgress."</span><span class="sxs-lookup"><span data-stu-id="5e8b5-158">A pending object can be deleted or overwritten by a create/import operation when its status is not "inProgress."</span></span>

|<span data-ttu-id="5e8b5-159">Method</span><span class="sxs-lookup"><span data-stu-id="5e8b5-159">Method</span></span>|<span data-ttu-id="5e8b5-160">Request URI</span><span class="sxs-lookup"><span data-stu-id="5e8b5-160">Request URI</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="5e8b5-161">GET</span><span class="sxs-lookup"><span data-stu-id="5e8b5-161">GET</span></span>|`https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}`|  

### <a name="request"></a><span data-ttu-id="5e8b5-162">Request</span><span class="sxs-lookup"><span data-stu-id="5e8b5-162">Request</span></span>  
 <span data-ttu-id="5e8b5-163">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"`</span><span class="sxs-lookup"><span data-stu-id="5e8b5-163">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"`</span></span>  

 <span data-ttu-id="5e8b5-164">OR</span><span class="sxs-lookup"><span data-stu-id="5e8b5-164">OR</span></span>  

 <span data-ttu-id="5e8b5-165">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}"`</span><span class="sxs-lookup"><span data-stu-id="5e8b5-165">GET `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}"`</span></span>  

### <a name="response"></a><span data-ttu-id="5e8b5-166">Response</span><span class="sxs-lookup"><span data-stu-id="5e8b5-166">Response</span></span>  

```  
StatusCode: 404, ReasonPhrase: 'Not Found'  
{  
  "error":  
    {  
         "code": "PendingCertificateNotFound",  
        "message": "…"  
    }  
}  

```  

## <a name="create-or-import-when-pending-request-exists---status-is-inprogress"></a><span data-ttu-id="5e8b5-167">Create (or Import) when pending request exists - status is "inProgress"</span><span class="sxs-lookup"><span data-stu-id="5e8b5-167">Create (or Import) when pending request exists - status is "inProgress"</span></span>
 <span data-ttu-id="5e8b5-168">A pending object has four possible states; "inprogress", "canceled", "failed", or "completed."</span><span class="sxs-lookup"><span data-stu-id="5e8b5-168">A pending object has four possible states; "inprogress", "canceled", "failed", or "completed."</span></span>

 <span data-ttu-id="5e8b5-169">When a pending request's state is "inprogress", create (and import) operations will fail with an http status code of 409 (conflict).</span><span class="sxs-lookup"><span data-stu-id="5e8b5-169">When a pending request's state is "inprogress", create (and import) operations will fail with an http status code of 409 (conflict).</span></span>  

 <span data-ttu-id="5e8b5-170">To fix a conflict:</span><span class="sxs-lookup"><span data-stu-id="5e8b5-170">To fix a conflict:</span></span>  

 - <span data-ttu-id="5e8b5-171">If the certificate is being manually created, you can either complete the KV certificate by doing a merge or delete on the pending object.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-171">If the certificate is being manually created, you can either complete the KV certificate by doing a merge or delete on the pending object.</span></span>  

 - <span data-ttu-id="5e8b5-172">If the certificate is being created with an issuer, you can wait until the certificate completes, fails or is canceled.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-172">If the certificate is being created with an issuer, you can wait until the certificate completes, fails or is canceled.</span></span> <span data-ttu-id="5e8b5-173">Alternatively, you can delete the pending object.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-173">Alternatively, you can delete the pending object.</span></span>

> [!NOTE]
> <span data-ttu-id="5e8b5-174">Deleting a pending object may or may not cancel the x509 certificate request with the provider.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-174">Deleting a pending object may or may not cancel the x509 certificate request with the provider.</span></span>  

|<span data-ttu-id="5e8b5-175">Method</span><span class="sxs-lookup"><span data-stu-id="5e8b5-175">Method</span></span>|<span data-ttu-id="5e8b5-176">Request URI</span><span class="sxs-lookup"><span data-stu-id="5e8b5-176">Request URI</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="5e8b5-177">POST</span><span class="sxs-lookup"><span data-stu-id="5e8b5-177">POST</span></span>|`https://mykeyvault.vault.azure.net/certificates/mycert1/create?api-version={api-version}`|  

### <a name="request"></a><span data-ttu-id="5e8b5-178">Request</span><span class="sxs-lookup"><span data-stu-id="5e8b5-178">Request</span></span>  

```json
{  
  "policy": {  
    "x509_props": {  
      "subject": "CN=MyCertSubject1"  
    },  
  "issuer": {  
       "name": "mydigicert"  
    }  
  }  
}  

```  

### <a name="response"></a><span data-ttu-id="5e8b5-179">Response</span><span class="sxs-lookup"><span data-stu-id="5e8b5-179">Response</span></span>  

```  
StatusCode: 409, ReasonPhrase: 'Conflict'  
{  
  "error":  
    {  
        "code": "Forbidden",  
        "message": "A new key vault certificate can not be created or imported while a pending key vault certificate's status is inProgress."  
    }  
}  

```  

## <a name="merge-when-pending-request-is-created-with-an-issuer"></a><span data-ttu-id="5e8b5-180">Merge when pending request is created with an issuer</span><span class="sxs-lookup"><span data-stu-id="5e8b5-180">Merge when pending request is created with an issuer</span></span>
 <span data-ttu-id="5e8b5-181">Merge is not allowed when a pending object is created with an issuer but is allowed when its state is "inProgress."</span><span class="sxs-lookup"><span data-stu-id="5e8b5-181">Merge is not allowed when a pending object is created with an issuer but is allowed when its state is "inProgress."</span></span> 

 <span data-ttu-id="5e8b5-182">If the request to create the x509 certificate fails or cancels for some reason, and if an x509 certificate can be retrieved by out-of-band means, a merge operation can be done to complete the KV certificate.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-182">If the request to create the x509 certificate fails or cancels for some reason, and if an x509 certificate can be retrieved by out-of-band means, a merge operation can be done to complete the KV certificate.</span></span>  

|<span data-ttu-id="5e8b5-183">Method</span><span class="sxs-lookup"><span data-stu-id="5e8b5-183">Method</span></span>|<span data-ttu-id="5e8b5-184">Request URI</span><span class="sxs-lookup"><span data-stu-id="5e8b5-184">Request URI</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="5e8b5-185">POST</span><span class="sxs-lookup"><span data-stu-id="5e8b5-185">POST</span></span>|`https://mykeyvault.vault.azure.net/certificates/mycert1/pending/merge?api-version={api-version}`|  

### <a name="request"></a><span data-ttu-id="5e8b5-186">Request</span><span class="sxs-lookup"><span data-stu-id="5e8b5-186">Request</span></span>  

```json
{  
  "x5c": [  "MIICxTCCAbi………………………trimmed for brevitiy……………………………………………EPAQj8="  
  ]  
}  

```  

### <a name="response"></a><span data-ttu-id="5e8b5-187">Response</span><span class="sxs-lookup"><span data-stu-id="5e8b5-187">Response</span></span>  

```json
StatusCode: 403, ReasonPhrase: 'Forbidden'  
{  
  "error":  
    {  
       "code": "Forbidden",  
       "message": "Merge is forbidden on pending object created with issuer : <issuer-name> while it is in progess."  
    }  
}  

```  

## <a name="request-a-cancellation-while-the-pending-request-status-is-inprogress"></a><span data-ttu-id="5e8b5-188">Request a cancellation while the pending request status is "inProgress"</span><span class="sxs-lookup"><span data-stu-id="5e8b5-188">Request a cancellation while the pending request status is "inProgress"</span></span>  
 <span data-ttu-id="5e8b5-189">A cancellation can only be requested.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-189">A cancellation can only be requested.</span></span>  <span data-ttu-id="5e8b5-190">A request may or may not be canceled.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-190">A request may or may not be canceled.</span></span> <span data-ttu-id="5e8b5-191">If a request is not "inProgress", an http status of 400 (Bad Request) is returned.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-191">If a request is not "inProgress", an http status of 400 (Bad Request) is returned.</span></span>  

|<span data-ttu-id="5e8b5-192">Method</span><span class="sxs-lookup"><span data-stu-id="5e8b5-192">Method</span></span>|<span data-ttu-id="5e8b5-193">Request URI</span><span class="sxs-lookup"><span data-stu-id="5e8b5-193">Request URI</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="5e8b5-194">PATCH</span><span class="sxs-lookup"><span data-stu-id="5e8b5-194">PATCH</span></span>|`https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}`|  

### <a name="request"></a><span data-ttu-id="5e8b5-195">Request</span><span class="sxs-lookup"><span data-stu-id="5e8b5-195">Request</span></span>  
 <span data-ttu-id="5e8b5-196">PATCH `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"`</span><span class="sxs-lookup"><span data-stu-id="5e8b5-196">PATCH `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"`</span></span>  

 <span data-ttu-id="5e8b5-197">OR</span><span class="sxs-lookup"><span data-stu-id="5e8b5-197">OR</span></span>  

 <span data-ttu-id="5e8b5-198">PATCH `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}"`</span><span class="sxs-lookup"><span data-stu-id="5e8b5-198">PATCH `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}"`</span></span>  

```json
{  
  "cancellation_requested": true  
}  

```  

### <a name="response"></a><span data-ttu-id="5e8b5-199">Response</span><span class="sxs-lookup"><span data-stu-id="5e8b5-199">Response</span></span>  

```  
StatusCode: 200, ReasonPhrase: 'OK'  
{  
  "id": “https://mykeyvault.vault.azure.net/certificates/mycert1/pending",  
  "issuer": {  
    "name": "{issuer-name}"  
  },  
  "csr": "MIICq......DD5Lp5cqXg==",  
  "cancellation_requested": true,  
  "status": "inProgress",  
  "status_details": "…",  
  "request_id": "a76827a18b63421c917da80f28e9913d"  
}  

```  

## <a name="delete-a-pending-request-object"></a><span data-ttu-id="5e8b5-200">Delete a pending request object</span><span class="sxs-lookup"><span data-stu-id="5e8b5-200">Delete a pending request object</span></span>  

> [!NOTE]
> <span data-ttu-id="5e8b5-201">Deleting the pending object may or may not cancel the x509 certificate request with the provider.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-201">Deleting the pending object may or may not cancel the x509 certificate request with the provider.</span></span>  

|<span data-ttu-id="5e8b5-202">Method</span><span class="sxs-lookup"><span data-stu-id="5e8b5-202">Method</span></span>|<span data-ttu-id="5e8b5-203">Request URI</span><span class="sxs-lookup"><span data-stu-id="5e8b5-203">Request URI</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="5e8b5-204">DELETE</span><span class="sxs-lookup"><span data-stu-id="5e8b5-204">DELETE</span></span>|`https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}`|  

### <a name="request"></a><span data-ttu-id="5e8b5-205">Request</span><span class="sxs-lookup"><span data-stu-id="5e8b5-205">Request</span></span>  
 <span data-ttu-id="5e8b5-206">DELETE `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"`</span><span class="sxs-lookup"><span data-stu-id="5e8b5-206">DELETE `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"`</span></span>  

 <span data-ttu-id="5e8b5-207">OR</span><span class="sxs-lookup"><span data-stu-id="5e8b5-207">OR</span></span>  

 <span data-ttu-id="5e8b5-208">DELETE `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}"`</span><span class="sxs-lookup"><span data-stu-id="5e8b5-208">DELETE `“https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}"`</span></span>  

### <a name="response"></a><span data-ttu-id="5e8b5-209">Response</span><span class="sxs-lookup"><span data-stu-id="5e8b5-209">Response</span></span>  

```  
StatusCode: 200, ReasonPhrase: 'OK'  
{  
  "id": “https://mykeyvault.vault.azure.net/certificates/mycert1/pending",  
  "issuer": {  
    "name": "{issuer-name}"  
  },  
  "csr": "MIICq......DD5Lp5cqXg==",  
  "cancellation_requested": false,  
  "status": "inProgress",  
  "request_id": "a76827a18b63421c917da80f28e9913d",  
}  
```  

## <a name="create-a-kv-certificate-manually"></a><span data-ttu-id="5e8b5-210">Create a KV certificate manually</span><span class="sxs-lookup"><span data-stu-id="5e8b5-210">Create a KV certificate manually</span></span>  
 <span data-ttu-id="5e8b5-211">You can create a certificate issued with a CA of your choice through a manual creation process.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-211">You can create a certificate issued with a CA of your choice through a manual creation process.</span></span> <span data-ttu-id="5e8b5-212">Set the name of the issuer to “Unknown” or do not specify the issuer field.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-212">Set the name of the issuer to “Unknown” or do not specify the issuer field.</span></span>  

|<span data-ttu-id="5e8b5-213">Method</span><span class="sxs-lookup"><span data-stu-id="5e8b5-213">Method</span></span>|<span data-ttu-id="5e8b5-214">Request URI</span><span class="sxs-lookup"><span data-stu-id="5e8b5-214">Request URI</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="5e8b5-215">POST</span><span class="sxs-lookup"><span data-stu-id="5e8b5-215">POST</span></span>|`https://mykeyvault.vault.azure.net/certificates/mycert1/create?api-version={api-version}`|  

### <a name="request"></a><span data-ttu-id="5e8b5-216">Request</span><span class="sxs-lookup"><span data-stu-id="5e8b5-216">Request</span></span>  

```json
{  
  "policy": {  
    "x509_props": {  
      "subject": "CN=MyCertSubject1"  
    }  
  "issuer": {  
       "name": "Unknown"  
    }  
  }  
}  

```  

### <a name="response"></a><span data-ttu-id="5e8b5-217">Response</span><span class="sxs-lookup"><span data-stu-id="5e8b5-217">Response</span></span>  

```  
StatusCode: 202, ReasonPhrase: 'Accepted'  
Location: “https://mykeyvault.vault.azure.net/certificates/mycert1/pending?api-version={api-version}&request_id=a76827a18b63421c917da80f28e9913d"  
{  
  "id": “https://mykeyvault.vault.azure.net/certificates/mycert1/pending",  
  "issuer": {  
    "name": "Unknown"  
  },  
  "csr": "MIICq......DD5Lp5cqXg==",  
  "status": "inProgress",  
  "status_details": "Pending certificate created. Please Perform Merge to complete the request.",  
  "request_id": "a76827a18b63421c917da80f28e9913d"  
}  

```  

## <a name="merge-when-a-pending-request-is-created---manual-certificate-creation"></a><span data-ttu-id="5e8b5-218">Merge when a pending request is created - manual certificate creation</span><span class="sxs-lookup"><span data-stu-id="5e8b5-218">Merge when a pending request is created - manual certificate creation</span></span>  

|<span data-ttu-id="5e8b5-219">Method</span><span class="sxs-lookup"><span data-stu-id="5e8b5-219">Method</span></span>|<span data-ttu-id="5e8b5-220">Request URI</span><span class="sxs-lookup"><span data-stu-id="5e8b5-220">Request URI</span></span>|  
|------------|-----------------|  
|<span data-ttu-id="5e8b5-221">POST</span><span class="sxs-lookup"><span data-stu-id="5e8b5-221">POST</span></span>|`https://mykeyvault.vault.azure.net/certificates/mycert1/pending/merge?api-version={api-version}`|  

### <a name="request"></a><span data-ttu-id="5e8b5-222">Request</span><span class="sxs-lookup"><span data-stu-id="5e8b5-222">Request</span></span>  

```json
{  
  "x5c": [  "MIICxTCCAbi………………………trimmed for brevitiy……………………………………………EPAQj8="  
  ]  
}  

```  

|Element name|Required|Type|Version|<span data-ttu-id="5e8b5-227">Description</span><span class="sxs-lookup"><span data-stu-id="5e8b5-227">Description</span></span>|  
|------------------|--------------|----------|-------------|-----------------|  
|<span data-ttu-id="5e8b5-228">x5c</span><span class="sxs-lookup"><span data-stu-id="5e8b5-228">x5c</span></span>|<span data-ttu-id="5e8b5-229">Yes</span><span class="sxs-lookup"><span data-stu-id="5e8b5-229">Yes</span></span>|<span data-ttu-id="5e8b5-230">array</span><span class="sxs-lookup"><span data-stu-id="5e8b5-230">array</span></span>|<span data-ttu-id="5e8b5-231">\<introducing version></span><span class="sxs-lookup"><span data-stu-id="5e8b5-231">\<introducing version></span></span>|<span data-ttu-id="5e8b5-232">X509 certificate chain as base 64 string array.</span><span class="sxs-lookup"><span data-stu-id="5e8b5-232">X509 certificate chain as base 64 string array.</span></span>|  

### <a name="response"></a><span data-ttu-id="5e8b5-233">Response</span><span class="sxs-lookup"><span data-stu-id="5e8b5-233">Response</span></span>  

```  
StatusCode: 201, ReasonPhrase: 'Created'  
Location: “https://mykeyvault.vault.azure.net/certificates/mycert1?api-version={api-version}"  
{  
"id": "https mykeyvault.vault.azure.net/certificates/mycert1/f366e1a9dd774288ad84a45a5f620352",  
    "kid": "https:// mykeyvault.vault.azure.net/keys/mycert1/f366e1a9dd774288ad84a45a5f620352",  
    "sid": " mykeyvault.vault.azure.net/secrets/mycert1/f366e1a9dd774288ad84a45a5f620352",  
    "cer": "……de34534……",  
    "x5t": "n14q2wbvyXr71Pcb58NivuiwJKk",  
    "attributes": {  
        "enabled": true,  
        "exp": 1530394215,  
        "nbf": 1435699215,  
        "created": 1435699919,  
        "updated": 1435699919  
    },  
    "pending": {  
        "id": "https:// mykeyvault.vault.azure.net/certificates/mycert1/pending"  
    },  
    "policy": {  
        "id": "https:// mykeyvault.vault.azure.net/certificates/mycert1/policy",  
        "key_props": {  
            "exportable": false,  
            "kty": "RSA",  
            "key_size": 2048,  
            "reuse_key": false  
        },  
        "secret_props": {  
            "contentType": "application/x-pkcs12"  
        },  
        "x509_props": {  
            "subject": "CN=Mycert1",  
            "ekus": ["1.3.6.1.5.5.7.3.1", "1.3.6.1.5.5.7.3.2"],  
                       "validity_months":12  
        },  
        "lifetime_actions": [{  
            "trigger": {  
                "lifetime_percentage": 80  
            },  
            "action": {  
                "action_type": "EmailContacts"  
            }  
        }],  
        "issuer": {  
            "name": "Unknown"  
        },  
        "attributes": {  
            "enabled": true,  
            "created": 1435699811,  
            "updated": 1435699811  
        }  
    }  
}  

```

## <a name="see-also"></a><span data-ttu-id="5e8b5-234">See Also</span><span class="sxs-lookup"><span data-stu-id="5e8b5-234">See Also</span></span>
- [<span data-ttu-id="5e8b5-235">About keys, secrets, and certificates</span><span class="sxs-lookup"><span data-stu-id="5e8b5-235">About keys, secrets, and certificates</span></span>](about-keys-secrets-and-certificates.md)
