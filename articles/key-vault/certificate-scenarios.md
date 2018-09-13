---
title: Get started with Key Vault certificates
description: The following scenarios outline several of the primary usages of Key Vault’s certificate management service including the additional steps required for creating your first certificate in your key vault.
services: key-vault
documentationcenter: ''
author: bryanla
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: a788b958-3acb-4bb6-9c94-4776852aeea1
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/09/2018
ms.author: bryanla
ms.openlocfilehash: d5cc634451c5412f9a3339c8d2d26654c4d5c1b8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865348"
---
# <a name="get-started-with-key-vault-certificates"></a><span data-ttu-id="7c29f-103">Get started with Key Vault certificates</span><span class="sxs-lookup"><span data-stu-id="7c29f-103">Get started with Key Vault certificates</span></span>
<span data-ttu-id="7c29f-104">The following scenarios outline several of the primary usages of Key Vault’s certificate management service including the additional steps required for creating your first certificate in your key vault.</span><span class="sxs-lookup"><span data-stu-id="7c29f-104">The following scenarios outline several of the primary usages of Key Vault’s certificate management service including the additional steps required for creating your first certificate in your key vault.</span></span>

<span data-ttu-id="7c29f-105">The following are outlined:</span><span class="sxs-lookup"><span data-stu-id="7c29f-105">The following are outlined:</span></span>
- <span data-ttu-id="7c29f-106">Creating your first Key Vault certificate</span><span class="sxs-lookup"><span data-stu-id="7c29f-106">Creating your first Key Vault certificate</span></span>
- <span data-ttu-id="7c29f-107">Creating a certificate with a Certificate Authority that is partnered with Key Vault</span><span class="sxs-lookup"><span data-stu-id="7c29f-107">Creating a certificate with a Certificate Authority that is partnered with Key Vault</span></span>
- <span data-ttu-id="7c29f-108">Creating a certificate with a Certificate Authority that is not partnered with Key Vault</span><span class="sxs-lookup"><span data-stu-id="7c29f-108">Creating a certificate with a Certificate Authority that is not partnered with Key Vault</span></span>
- <span data-ttu-id="7c29f-109">Import a certificate</span><span class="sxs-lookup"><span data-stu-id="7c29f-109">Import a certificate</span></span>

## <a name="certificates-are-complex-objects"></a><span data-ttu-id="7c29f-110">Certificates are complex objects</span><span class="sxs-lookup"><span data-stu-id="7c29f-110">Certificates are complex objects</span></span>
<span data-ttu-id="7c29f-111">Certificates are composed of three interrelated resources linked together as a Key Vault certificate; certificate metadata, a key, and a secret.</span><span class="sxs-lookup"><span data-stu-id="7c29f-111">Certificates are composed of three interrelated resources linked together as a Key Vault certificate; certificate metadata, a key, and a secret.</span></span>


![Certificates are complex](media/azure-key-vault.png)


## <a name="creating-your-first-key-vault-certificate"></a><span data-ttu-id="7c29f-113">Creating your first Key Vault certificate</span><span class="sxs-lookup"><span data-stu-id="7c29f-113">Creating your first Key Vault certificate</span></span>  
 <span data-ttu-id="7c29f-114">Before a certificate can be created in a Key Vault (KV), prerequisite steps 1 and 2 must be successfully accomplished and a key vault must exist for this user / organization.</span><span class="sxs-lookup"><span data-stu-id="7c29f-114">Before a certificate can be created in a Key Vault (KV), prerequisite steps 1 and 2 must be successfully accomplished and a key vault must exist for this user / organization.</span></span>  

<span data-ttu-id="7c29f-115">**Step 1** - Certificate Authority (CA) Providers</span><span class="sxs-lookup"><span data-stu-id="7c29f-115">**Step 1** - Certificate Authority (CA) Providers</span></span>  
-   <span data-ttu-id="7c29f-116">On-boarding as the IT Admin, PKI Admin or anyone managing accounts with CAs, for a given company (ex.</span><span class="sxs-lookup"><span data-stu-id="7c29f-116">On-boarding as the IT Admin, PKI Admin or anyone managing accounts with CAs, for a given company (ex.</span></span> <span data-ttu-id="7c29f-117">Contoso)  is a prerequisite to using Key Vault certificates.</span><span class="sxs-lookup"><span data-stu-id="7c29f-117">Contoso)  is a prerequisite to using Key Vault certificates.</span></span>  
    <span data-ttu-id="7c29f-118">The following CAs are the current partnered providers with Key Vault:</span><span class="sxs-lookup"><span data-stu-id="7c29f-118">The following CAs are the current partnered providers with Key Vault:</span></span>  
    -   <span data-ttu-id="7c29f-119">DigiCert - Key Vault offers OV SSL certificates with DigiCert.</span><span class="sxs-lookup"><span data-stu-id="7c29f-119">DigiCert - Key Vault offers OV SSL certificates with DigiCert.</span></span>  
    -   <span data-ttu-id="7c29f-120">GlobalSign - Key Vault offers OV SSL certificates with GlobalSign</span><span class="sxs-lookup"><span data-stu-id="7c29f-120">GlobalSign - Key Vault offers OV SSL certificates with GlobalSign</span></span>  
    -   <span data-ttu-id="7c29f-121">WoSign - Key Vault offers OV SSL or EV SSL certificates with WoSign based on setting configured by customer in their WoSign account on the WoSign portal.</span><span class="sxs-lookup"><span data-stu-id="7c29f-121">WoSign - Key Vault offers OV SSL or EV SSL certificates with WoSign based on setting configured by customer in their WoSign account on the WoSign portal.</span></span>  

<span data-ttu-id="7c29f-122">**Step 2** - An account admin for a CA provider creates credentials to be used by Key Vault to enroll, renew, and use SSL certificates via Key Vault.</span><span class="sxs-lookup"><span data-stu-id="7c29f-122">**Step 2** - An account admin for a CA provider creates credentials to be used by Key Vault to enroll, renew, and use SSL certificates via Key Vault.</span></span>

<span data-ttu-id="7c29f-123">**Step 3** - A Contoso admin, along with a Contoso employee (Key Vault user) who owns certificates, depending on the CA, can get a certificate from the admin or directly from the account with the CA.</span><span class="sxs-lookup"><span data-stu-id="7c29f-123">**Step 3** - A Contoso admin, along with a Contoso employee (Key Vault user) who owns certificates, depending on the CA, can get a certificate from the admin or directly from the account with the CA.</span></span>  

-   <span data-ttu-id="7c29f-124">Begin an add credential operation to a key vault by [setting a certificate issuer](/rest/api/keyvault/setcertificateissuer) resource.</span><span class="sxs-lookup"><span data-stu-id="7c29f-124">Begin an add credential operation to a key vault by [setting a certificate issuer](/rest/api/keyvault/setcertificateissuer) resource.</span></span> <span data-ttu-id="7c29f-125">A certificate issuer is an entity represented in Azure Key Vault (KV) as a CertificateIssuer resource.</span><span class="sxs-lookup"><span data-stu-id="7c29f-125">A certificate issuer is an entity represented in Azure Key Vault (KV) as a CertificateIssuer resource.</span></span> <span data-ttu-id="7c29f-126">It is used to provide information about the source of a KV certificate; issuer name, provider, credentials, and other administrative details.</span><span class="sxs-lookup"><span data-stu-id="7c29f-126">It is used to provide information about the source of a KV certificate; issuer name, provider, credentials, and other administrative details.</span></span>
    -   <span data-ttu-id="7c29f-127">Ex.</span><span class="sxs-lookup"><span data-stu-id="7c29f-127">Ex.</span></span> <span data-ttu-id="7c29f-128">MyDigiCertIssuer</span><span class="sxs-lookup"><span data-stu-id="7c29f-128">MyDigiCertIssuer</span></span>  
        -   <span data-ttu-id="7c29f-129">Provider</span><span class="sxs-lookup"><span data-stu-id="7c29f-129">Provider</span></span>  
        -   <span data-ttu-id="7c29f-130">Credentials – CA account credentials.</span><span class="sxs-lookup"><span data-stu-id="7c29f-130">Credentials – CA account credentials.</span></span> <span data-ttu-id="7c29f-131">Each CA has its own specific data.</span><span class="sxs-lookup"><span data-stu-id="7c29f-131">Each CA has its own specific data.</span></span>  

     <span data-ttu-id="7c29f-132">For more information on creating accounts with CA Providers, see the related post on the [Key Vault blog](http://aka.ms/kvcertsblog).</span><span class="sxs-lookup"><span data-stu-id="7c29f-132">For more information on creating accounts with CA Providers, see the related post on the [Key Vault blog](http://aka.ms/kvcertsblog).</span></span>  

<span data-ttu-id="7c29f-133">**Step 3.1** - set up [certificate contacts](/rest/api/keyvault/setcertificatecontacts) for notifications.</span><span class="sxs-lookup"><span data-stu-id="7c29f-133">**Step 3.1** - set up [certificate contacts](/rest/api/keyvault/setcertificatecontacts) for notifications.</span></span> <span data-ttu-id="7c29f-134">This is the contact for the Key Vault user.</span><span class="sxs-lookup"><span data-stu-id="7c29f-134">This is the contact for the Key Vault user.</span></span> <span data-ttu-id="7c29f-135">Key Vault does not enforce this step.</span><span class="sxs-lookup"><span data-stu-id="7c29f-135">Key Vault does not enforce this step.</span></span>  

<span data-ttu-id="7c29f-136">Note - This process, through step 3.1, is a onetime operation.</span><span class="sxs-lookup"><span data-stu-id="7c29f-136">Note - This process, through step 3.1, is a onetime operation.</span></span>  

## <a name="creating-a-certificate-with-a-ca-partnered-with-key-vault"></a><span data-ttu-id="7c29f-137">Creating a certificate with a CA partnered with Key Vault</span><span class="sxs-lookup"><span data-stu-id="7c29f-137">Creating a certificate with a CA partnered with Key Vault</span></span>

![Create a certificate with a Key Vault partnered certificate authority](media/certificate-authority-2.png)

<span data-ttu-id="7c29f-139">**Step 4** - The following descriptions correspond to the green numbered steps in the preceding diagram.</span><span class="sxs-lookup"><span data-stu-id="7c29f-139">**Step 4** - The following descriptions correspond to the green numbered steps in the preceding diagram.</span></span>  
  <span data-ttu-id="7c29f-140">(1) - In the diagram above, your application is creating a certificate which internally begins by creating a key in your key vault.</span><span class="sxs-lookup"><span data-stu-id="7c29f-140">(1) - In the diagram above, your application is creating a certificate which internally begins by creating a key in your key vault.</span></span>  
  <span data-ttu-id="7c29f-141">(2) - Key Vault sends an SSL Certificate Request to the CA.</span><span class="sxs-lookup"><span data-stu-id="7c29f-141">(2) - Key Vault sends an SSL Certificate Request to the CA.</span></span>  
  <span data-ttu-id="7c29f-142">(3) - Your application polls, in a loop and wait process, for your Key Vault for certificate completion.</span><span class="sxs-lookup"><span data-stu-id="7c29f-142">(3) - Your application polls, in a loop and wait process, for your Key Vault for certificate completion.</span></span> <span data-ttu-id="7c29f-143">The certificate creation is complete when Key Vault receives the CA’s response with x509 certificate.</span><span class="sxs-lookup"><span data-stu-id="7c29f-143">The certificate creation is complete when Key Vault receives the CA’s response with x509 certificate.</span></span>  
  <span data-ttu-id="7c29f-144">(4) - The CA responds to Key Vault's SSL Certificate Request with an X509 SSL Certificate.</span><span class="sxs-lookup"><span data-stu-id="7c29f-144">(4) - The CA responds to Key Vault's SSL Certificate Request with an X509 SSL Certificate.</span></span>  
  <span data-ttu-id="7c29f-145">(5) - Your new certificate creation completes with the merger of the X509 Certificate for the CA.</span><span class="sxs-lookup"><span data-stu-id="7c29f-145">(5) - Your new certificate creation completes with the merger of the X509 Certificate for the CA.</span></span>  

  <span data-ttu-id="7c29f-146">Key Vault user – creates a certificate by specifying a policy</span><span class="sxs-lookup"><span data-stu-id="7c29f-146">Key Vault user – creates a certificate by specifying a policy</span></span>

  -   <span data-ttu-id="7c29f-147">Repeat as needed</span><span class="sxs-lookup"><span data-stu-id="7c29f-147">Repeat as needed</span></span>  
  -   <span data-ttu-id="7c29f-148">Policy constraints</span><span class="sxs-lookup"><span data-stu-id="7c29f-148">Policy constraints</span></span>  
      -   <span data-ttu-id="7c29f-149">X509 properties</span><span class="sxs-lookup"><span data-stu-id="7c29f-149">X509 properties</span></span>  
      -   <span data-ttu-id="7c29f-150">Key properties</span><span class="sxs-lookup"><span data-stu-id="7c29f-150">Key properties</span></span>  
      -   <span data-ttu-id="7c29f-151">Provider reference - > ex.</span><span class="sxs-lookup"><span data-stu-id="7c29f-151">Provider reference - > ex.</span></span> <span data-ttu-id="7c29f-152">MyDigiCertIssure</span><span class="sxs-lookup"><span data-stu-id="7c29f-152">MyDigiCertIssure</span></span>  
      -   <span data-ttu-id="7c29f-153">Renewal information - > ex.</span><span class="sxs-lookup"><span data-stu-id="7c29f-153">Renewal information - > ex.</span></span> <span data-ttu-id="7c29f-154">90 days before expiry</span><span class="sxs-lookup"><span data-stu-id="7c29f-154">90 days before expiry</span></span>  

  - <span data-ttu-id="7c29f-155">A certificate creation process is usually an asynchronous process and involves polling your key vault for the state of the create certificate operation.</span><span class="sxs-lookup"><span data-stu-id="7c29f-155">A certificate creation process is usually an asynchronous process and involves polling your key vault for the state of the create certificate operation.</span></span>  
[<span data-ttu-id="7c29f-156">Get certificate operation</span><span class="sxs-lookup"><span data-stu-id="7c29f-156">Get certificate operation</span></span>](https://docs.microsoft.com/en-us/rest/api/keyvault/getcertificateoperation)  
      -   <span data-ttu-id="7c29f-157">Status: completed, failed with error information or, canceled</span><span class="sxs-lookup"><span data-stu-id="7c29f-157">Status: completed, failed with error information or, canceled</span></span>  
      -   <span data-ttu-id="7c29f-158">Because of the delay to create, a cancel operation can be initiated.</span><span class="sxs-lookup"><span data-stu-id="7c29f-158">Because of the delay to create, a cancel operation can be initiated.</span></span> <span data-ttu-id="7c29f-159">The cancel may or may not be effective.</span><span class="sxs-lookup"><span data-stu-id="7c29f-159">The cancel may or may not be effective.</span></span>  

## <a name="import-a-certificate"></a><span data-ttu-id="7c29f-160">Import a certificate</span><span class="sxs-lookup"><span data-stu-id="7c29f-160">Import a certificate</span></span>  
 <span data-ttu-id="7c29f-161">Alternatively – a cert can be imported into Key Vault – PFX or PEM.</span><span class="sxs-lookup"><span data-stu-id="7c29f-161">Alternatively – a cert can be imported into Key Vault – PFX or PEM.</span></span>  

 <span data-ttu-id="7c29f-162">For more information on PEM format, see the certificates section of [About keys, secrets, and certificates](about-keys-secrets-and-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="7c29f-162">For more information on PEM format, see the certificates section of [About keys, secrets, and certificates](about-keys-secrets-and-certificates.md).</span></span>  

 <span data-ttu-id="7c29f-163">Import certificate – requires a PEM or PFX to be on disk and have a private key.</span><span class="sxs-lookup"><span data-stu-id="7c29f-163">Import certificate – requires a PEM or PFX to be on disk and have a private key.</span></span> 
-   <span data-ttu-id="7c29f-164">You must specify: vault name and certificate name (policy is optional)</span><span class="sxs-lookup"><span data-stu-id="7c29f-164">You must specify: vault name and certificate name (policy is optional)</span></span>

-   <span data-ttu-id="7c29f-165">PEM / PFX files contains attributes that KV can parse and use to populate the certificate policy.</span><span class="sxs-lookup"><span data-stu-id="7c29f-165">PEM / PFX files contains attributes that KV can parse and use to populate the certificate policy.</span></span> <span data-ttu-id="7c29f-166">If a certificate policy is already specified, KV will try to match data from PFX  / PEM file.</span><span class="sxs-lookup"><span data-stu-id="7c29f-166">If a certificate policy is already specified, KV will try to match data from PFX  / PEM file.</span></span>  

-   <span data-ttu-id="7c29f-167">Once the import is final, subsequent operations will use the new policy (new versions).</span><span class="sxs-lookup"><span data-stu-id="7c29f-167">Once the import is final, subsequent operations will use the new policy (new versions).</span></span>  

-   <span data-ttu-id="7c29f-168">If there are no further operations, the first thing the Key Vault does is send an expiration notice.</span><span class="sxs-lookup"><span data-stu-id="7c29f-168">If there are no further operations, the first thing the Key Vault does is send an expiration notice.</span></span> 

-   <span data-ttu-id="7c29f-169">Also, the user can edit the policy, which is functional at the time of import but, contains defaults where no information was specified at import.</span><span class="sxs-lookup"><span data-stu-id="7c29f-169">Also, the user can edit the policy, which is functional at the time of import but, contains defaults where no information was specified at import.</span></span> <span data-ttu-id="7c29f-170">Ex.</span><span class="sxs-lookup"><span data-stu-id="7c29f-170">Ex.</span></span> <span data-ttu-id="7c29f-171">no issuer info</span><span class="sxs-lookup"><span data-stu-id="7c29f-171">no issuer info</span></span>  

## <a name="creating-a-certificate-with-a-ca-not-partnered-with-key-vault"></a><span data-ttu-id="7c29f-172">Creating a certificate with a CA not partnered with Key Vault</span><span class="sxs-lookup"><span data-stu-id="7c29f-172">Creating a certificate with a CA not partnered with Key Vault</span></span>  
 <span data-ttu-id="7c29f-173">This method allows working with other CAs than Key Vault's partnered providers, meaning your organization can work with a CA of its choice.</span><span class="sxs-lookup"><span data-stu-id="7c29f-173">This method allows working with other CAs than Key Vault's partnered providers, meaning your organization can work with a CA of its choice.</span></span>  

![Create a certificate with your own certificate authority](media/certificate-authority-1.png)  

 <span data-ttu-id="7c29f-175">The following step descriptions correspond to the green lettered steps in the preceding diagram.</span><span class="sxs-lookup"><span data-stu-id="7c29f-175">The following step descriptions correspond to the green lettered steps in the preceding diagram.</span></span>  

  <span data-ttu-id="7c29f-176">(1) - In the diagram above, your application is creating a certificate, which internally begins by creating a key in your key vault.</span><span class="sxs-lookup"><span data-stu-id="7c29f-176">(1) - In the diagram above, your application is creating a certificate, which internally begins by creating a key in your key vault.</span></span>  

  <span data-ttu-id="7c29f-177">(2) - Key Vault returns to your application a Certificate Signing Request (CSR).</span><span class="sxs-lookup"><span data-stu-id="7c29f-177">(2) - Key Vault returns to your application a Certificate Signing Request (CSR).</span></span>  

  <span data-ttu-id="7c29f-178">(3) - Your application passes the CSR to your chosen CA.</span><span class="sxs-lookup"><span data-stu-id="7c29f-178">(3) - Your application passes the CSR to your chosen CA.</span></span>  

  <span data-ttu-id="7c29f-179">(4) - Your chosen CA responds with an X509 Certificate.</span><span class="sxs-lookup"><span data-stu-id="7c29f-179">(4) - Your chosen CA responds with an X509 Certificate.</span></span>  

  <span data-ttu-id="7c29f-180">(5) - Your application completes the new certificate creation with a merger of the X509 Certificate from your CA.</span><span class="sxs-lookup"><span data-stu-id="7c29f-180">(5) - Your application completes the new certificate creation with a merger of the X509 Certificate from your CA.</span></span>

## <a name="see-also"></a><span data-ttu-id="7c29f-181">See Also</span><span class="sxs-lookup"><span data-stu-id="7c29f-181">See Also</span></span>

- [<span data-ttu-id="7c29f-182">About keys, secrets, and certificates</span><span class="sxs-lookup"><span data-stu-id="7c29f-182">About keys, secrets, and certificates</span></span>](about-keys-secrets-and-certificates.md)
