---
title: Encrypting your content with storage encryption using AMS REST API
description: Learn how to encrypt your content with storage encryption using AMS REST APIs.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: a0a79f3d-76a1-4994-9202-59b91a2230e0
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2018
ms.author: juliako
ms.openlocfilehash: 12c7559f0fab2cda9a97c2edf3e3206448b787c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869822"
---
# <a name="encrypting-your-content-with-storage-encryption"></a><span data-ttu-id="a9fd2-103">Encrypting your content with storage encryption</span><span class="sxs-lookup"><span data-stu-id="a9fd2-103">Encrypting your content with storage encryption</span></span>

<span data-ttu-id="a9fd2-104">It is highly recommended to encrypt your content locally using AES-256 bit encryption and then upload it to Azure Storage where it is stored encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-104">It is highly recommended to encrypt your content locally using AES-256 bit encryption and then upload it to Azure Storage where it is stored encrypted at rest.</span></span>

<span data-ttu-id="a9fd2-105">This article gives an overview of AMS storage encryption and shows you how to upload the storage encrypted content:</span><span class="sxs-lookup"><span data-stu-id="a9fd2-105">This article gives an overview of AMS storage encryption and shows you how to upload the storage encrypted content:</span></span>

* <span data-ttu-id="a9fd2-106">Create a content key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-106">Create a content key.</span></span>
* <span data-ttu-id="a9fd2-107">Create an Asset.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-107">Create an Asset.</span></span> <span data-ttu-id="a9fd2-108">Set the AssetCreationOption to StorageEncryption when creating the Asset.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-108">Set the AssetCreationOption to StorageEncryption when creating the Asset.</span></span>
  
     <span data-ttu-id="a9fd2-109">Encrypted assets are associated with content keys.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-109">Encrypted assets are associated with content keys.</span></span>
* <span data-ttu-id="a9fd2-110">Link the content key to the asset.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-110">Link the content key to the asset.</span></span>  
* <span data-ttu-id="a9fd2-111">Set the encryption-related parameters on the AssetFile entities.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-111">Set the encryption-related parameters on the AssetFile entities.</span></span>

## <a name="considerations"></a><span data-ttu-id="a9fd2-112">Considerations</span><span class="sxs-lookup"><span data-stu-id="a9fd2-112">Considerations</span></span> 

<span data-ttu-id="a9fd2-113">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-113">If you want to deliver a storage encrypted asset, you must configure the asset’s delivery policy.</span></span> <span data-ttu-id="a9fd2-114">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-114">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy.</span></span> <span data-ttu-id="a9fd2-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a9fd2-115">For more information, see [Configuring Asset Delivery Policies](media-services-rest-configure-asset-delivery-policy.md).</span></span>

<span data-ttu-id="a9fd2-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-116">When accessing entities in Media Services, you must set specific header fields and values in your HTTP requests.</span></span> <span data-ttu-id="a9fd2-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="a9fd2-117">For more information, see [Setup for Media Services REST API Development](media-services-rest-how-to-use.md).</span></span> 

### <a name="storage-side-encryption"></a><span data-ttu-id="a9fd2-118">Storage side encryption</span><span class="sxs-lookup"><span data-stu-id="a9fd2-118">Storage side encryption</span></span>

|<span data-ttu-id="a9fd2-119">Encryption option</span><span class="sxs-lookup"><span data-stu-id="a9fd2-119">Encryption option</span></span>|<span data-ttu-id="a9fd2-120">Description</span><span class="sxs-lookup"><span data-stu-id="a9fd2-120">Description</span></span>|<span data-ttu-id="a9fd2-121">Media Services v2</span><span class="sxs-lookup"><span data-stu-id="a9fd2-121">Media Services v2</span></span>|<span data-ttu-id="a9fd2-122">Media Services v3</span><span class="sxs-lookup"><span data-stu-id="a9fd2-122">Media Services v3</span></span>|
|---|---|---|---|
|<span data-ttu-id="a9fd2-123">Media Services Storage Encryption</span><span class="sxs-lookup"><span data-stu-id="a9fd2-123">Media Services Storage Encryption</span></span>|<span data-ttu-id="a9fd2-124">AES-256 encryption, key managed by Media Services</span><span class="sxs-lookup"><span data-stu-id="a9fd2-124">AES-256 encryption, key managed by Media Services</span></span>|<span data-ttu-id="a9fd2-125">Supported<sup>(1)</sup></span><span class="sxs-lookup"><span data-stu-id="a9fd2-125">Supported<sup>(1)</sup></span></span>|<span data-ttu-id="a9fd2-126">Not supported<sup>(2)</sup></span><span class="sxs-lookup"><span data-stu-id="a9fd2-126">Not supported<sup>(2)</sup></span></span>|
|[<span data-ttu-id="a9fd2-127">Storage Service Encryption for Data at Rest</span><span class="sxs-lookup"><span data-stu-id="a9fd2-127">Storage Service Encryption for Data at Rest</span></span>](https://docs.microsoft.com/azure/storage/common/storage-service-encryption)|<span data-ttu-id="a9fd2-128">Server-side encryption offered by Azure Storage, key managed by Azure or by customer</span><span class="sxs-lookup"><span data-stu-id="a9fd2-128">Server-side encryption offered by Azure Storage, key managed by Azure or by customer</span></span>|<span data-ttu-id="a9fd2-129">Supported</span><span class="sxs-lookup"><span data-stu-id="a9fd2-129">Supported</span></span>|<span data-ttu-id="a9fd2-130">Supported</span><span class="sxs-lookup"><span data-stu-id="a9fd2-130">Supported</span></span>|
|[<span data-ttu-id="a9fd2-131">Storage Client-Side Encryption</span><span class="sxs-lookup"><span data-stu-id="a9fd2-131">Storage Client-Side Encryption</span></span>](https://docs.microsoft.com/azure/storage/common/storage-client-side-encryption)|<span data-ttu-id="a9fd2-132">Client-side encryption offered by Azure storage, key managed by customer in Key Vault</span><span class="sxs-lookup"><span data-stu-id="a9fd2-132">Client-side encryption offered by Azure storage, key managed by customer in Key Vault</span></span>|<span data-ttu-id="a9fd2-133">Not supported</span><span class="sxs-lookup"><span data-stu-id="a9fd2-133">Not supported</span></span>|<span data-ttu-id="a9fd2-134">Not supported</span><span class="sxs-lookup"><span data-stu-id="a9fd2-134">Not supported</span></span>|

<span data-ttu-id="a9fd2-135"><sup>1</sup> While Media Services does support handling of content in the clear/without any form of encryption, doing so is not recommended.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-135"><sup>1</sup> While Media Services does support handling of content in the clear/without any form of encryption, doing so is not recommended.</span></span>

<span data-ttu-id="a9fd2-136"><sup>2</sup> In Media Services v3, storage encryption (AES-256 encryption) is only supported for backwards compatibility when your Assets were created with Media Services v2.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-136"><sup>2</sup> In Media Services v3, storage encryption (AES-256 encryption) is only supported for backwards compatibility when your Assets were created with Media Services v2.</span></span> <span data-ttu-id="a9fd2-137">Meaning v3 works with existing storage encrypted assets but will not allow creation of new ones.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-137">Meaning v3 works with existing storage encrypted assets but will not allow creation of new ones.</span></span>

## <a name="connect-to-media-services"></a><span data-ttu-id="a9fd2-138">Connect to Media Services</span><span class="sxs-lookup"><span data-stu-id="a9fd2-138">Connect to Media Services</span></span>

<span data-ttu-id="a9fd2-139">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="a9fd2-139">For information on how to connect to the AMS API, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

## <a name="storage-encryption-overview"></a><span data-ttu-id="a9fd2-140">Storage encryption overview</span><span class="sxs-lookup"><span data-stu-id="a9fd2-140">Storage encryption overview</span></span>
<span data-ttu-id="a9fd2-141">The AMS storage encryption applies **AES-CTR** mode encryption to the entire file.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-141">The AMS storage encryption applies **AES-CTR** mode encryption to the entire file.</span></span>  <span data-ttu-id="a9fd2-142">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-142">AES-CTR mode is a block cipher that can encrypt arbitrary length data without need for padding.</span></span> <span data-ttu-id="a9fd2-143">It operates by encrypting a counter block with the AES algorithm and then XOR-ing the output of AES with the data to encrypt or decrypt.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-143">It operates by encrypting a counter block with the AES algorithm and then XOR-ing the output of AES with the data to encrypt or decrypt.</span></span>  <span data-ttu-id="a9fd2-144">The counter block used is constructed by copying the value of the InitializationVector to bytes 0 to 7 of the counter value and bytes 8 to 15 of the counter value are set to zero.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-144">The counter block used is constructed by copying the value of the InitializationVector to bytes 0 to 7 of the counter value and bytes 8 to 15 of the counter value are set to zero.</span></span> <span data-ttu-id="a9fd2-145">Of the 16-byte counter block, bytes 8 to 15 (that is, the least significant bytes) are used as a simple 64-bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-145">Of the 16-byte counter block, bytes 8 to 15 (that is, the least significant bytes) are used as a simple 64-bit unsigned integer that is incremented by one for each subsequent block of data processed and is kept in network byte order.</span></span> <span data-ttu-id="a9fd2-146">If this integer reaches the maximum value (0xFFFFFFFFFFFFFFFF), then incrementing it resets the block counter to zero (bytes 8 to 15) without affecting the other 64 bits of the counter (that is, bytes 0 to 7).</span><span class="sxs-lookup"><span data-stu-id="a9fd2-146">If this integer reaches the maximum value (0xFFFFFFFFFFFFFFFF), then incrementing it resets the block counter to zero (bytes 8 to 15) without affecting the other 64 bits of the counter (that is, bytes 0 to 7).</span></span>   <span data-ttu-id="a9fd2-147">In order to maintain the security of the AES-CTR mode encryption, the InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-147">In order to maintain the security of the AES-CTR mode encryption, the InitializationVector value for a given Key Identifier for each content key shall be unique for each file and files shall be less than 2^64 blocks in length.</span></span>  <span data-ttu-id="a9fd2-148">This unique value is to ensure that a counter value is never reused with a given key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-148">This unique value is to ensure that a counter value is never reused with a given key.</span></span> <span data-ttu-id="a9fd2-149">For more information about the CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (the wiki article uses the term "Nonce" instead of "InitializationVector").</span><span class="sxs-lookup"><span data-stu-id="a9fd2-149">For more information about the CTR mode, see [this wiki page](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#CTR) (the wiki article uses the term "Nonce" instead of "InitializationVector").</span></span>

<span data-ttu-id="a9fd2-150">Use **Storage Encryption** to encrypt your clear content locally using AES-256 bit encryption and then upload it to Azure Storage where it is stored encrypted at rest.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-150">Use **Storage Encryption** to encrypt your clear content locally using AES-256 bit encryption and then upload it to Azure Storage where it is stored encrypted at rest.</span></span> <span data-ttu-id="a9fd2-151">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-151">Assets protected with storage encryption are automatically unencrypted and placed in an encrypted file system prior to encoding, and optionally re-encrypted prior to uploading back as a new output asset.</span></span> <span data-ttu-id="a9fd2-152">The primary use case for storage encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-152">The primary use case for storage encryption is when you want to secure your high-quality input media files with strong encryption at rest on disk.</span></span>

<span data-ttu-id="a9fd2-153">In order to deliver a storage encrypted asset, you must configure the asset’s delivery policy so Media Services knows how you want to deliver your content.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-153">In order to deliver a storage encrypted asset, you must configure the asset’s delivery policy so Media Services knows how you want to deliver your content.</span></span> <span data-ttu-id="a9fd2-154">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy (for example, AES, common encryption, or no encryption).</span><span class="sxs-lookup"><span data-stu-id="a9fd2-154">Before your asset can be streamed, the streaming server removes the storage encryption and streams your content using the specified delivery policy (for example, AES, common encryption, or no encryption).</span></span>

## <a name="create-contentkeys-used-for-encryption"></a><span data-ttu-id="a9fd2-155">Create ContentKeys used for encryption</span><span class="sxs-lookup"><span data-stu-id="a9fd2-155">Create ContentKeys used for encryption</span></span>
<span data-ttu-id="a9fd2-156">Encrypted assets are associated with Storage Encryption keys.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-156">Encrypted assets are associated with Storage Encryption keys.</span></span> <span data-ttu-id="a9fd2-157">Create the content key to be used for encryption before creating the asset files.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-157">Create the content key to be used for encryption before creating the asset files.</span></span> <span data-ttu-id="a9fd2-158">This section describes how to create a content key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-158">This section describes how to create a content key.</span></span>

<span data-ttu-id="a9fd2-159">The following are general steps for generating content keys that you associate with assets that you want to be encrypted.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-159">The following are general steps for generating content keys that you associate with assets that you want to be encrypted.</span></span> 

1. <span data-ttu-id="a9fd2-160">For storage encryption, randomly generate a 32-byte AES key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-160">For storage encryption, randomly generate a 32-byte AES key.</span></span> 
   
    <span data-ttu-id="a9fd2-161">The 32-byte AES Key is the content key for your asset, which means all files associated with that asset need to use the same content key during decryption.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-161">The 32-byte AES Key is the content key for your asset, which means all files associated with that asset need to use the same content key during decryption.</span></span> 
2. <span data-ttu-id="a9fd2-162">Call the [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods to get the correct X.509 Certificate that must be used to encrypt your content key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-162">Call the [GetProtectionKeyId](https://docs.microsoft.com/rest/api/media/operations/rest-api-functions#getprotectionkeyid) and [GetProtectionKey](https://msdn.microsoft.com/library/azure/jj683097.aspx#getprotectionkey) methods to get the correct X.509 Certificate that must be used to encrypt your content key.</span></span>
3. <span data-ttu-id="a9fd2-163">Encrypt your content key with the public key of the X.509 Certificate.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-163">Encrypt your content key with the public key of the X.509 Certificate.</span></span> 
   
   <span data-ttu-id="a9fd2-164">Media Services .NET SDK uses RSA with OAEP when doing the encryption.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-164">Media Services .NET SDK uses RSA with OAEP when doing the encryption.</span></span>  <span data-ttu-id="a9fd2-165">You can see a .NET example in the [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="a9fd2-165">You can see a .NET example in the [EncryptSymmetricKeyData function](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
4. <span data-ttu-id="a9fd2-166">Create a checksum value calculated using the key identifier and content key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-166">Create a checksum value calculated using the key identifier and content key.</span></span> <span data-ttu-id="a9fd2-167">The following .NET example calculates the checksum using the GUID part of the key identifier and the clear content key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-167">The following .NET example calculates the checksum using the GUID part of the key identifier and the clear content key.</span></span>

    ```csharp
            public static string CalculateChecksum(byte[] contentKey, Guid keyId)
            {
                const int ChecksumLength = 8;
                const int KeyIdLength = 16;

                byte[] encryptedKeyId = null;

                // Checksum is computed by AES-ECB encrypting the KID
                // with the content key.
                using (AesCryptoServiceProvider rijndael = new AesCryptoServiceProvider())
                {
                    rijndael.Mode = CipherMode.ECB;
                    rijndael.Key = contentKey;
                    rijndael.Padding = PaddingMode.None;

                    ICryptoTransform encryptor = rijndael.CreateEncryptor();
                    encryptedKeyId = new byte[KeyIdLength];
                    encryptor.TransformBlock(keyId.ToByteArray(), 0, KeyIdLength, encryptedKeyId, 0);
                }

                byte[] retVal = new byte[ChecksumLength];
                Array.Copy(encryptedKeyId, retVal, ChecksumLength);

                return Convert.ToBase64String(retVal);
            }
    ```

5. <span data-ttu-id="a9fd2-168">Create the Content key with the **EncryptedContentKey** (converted to base64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-168">Create the Content key with the **EncryptedContentKey** (converted to base64-encoded string), **ProtectionKeyId**, **ProtectionKeyType**, **ContentKeyType**, and **Checksum** values you have received in previous steps.</span></span>

    <span data-ttu-id="a9fd2-169">For storage encryption, the following properties should be included in the request body.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-169">For storage encryption, the following properties should be included in the request body.</span></span>

    <span data-ttu-id="a9fd2-170">Request body property</span><span class="sxs-lookup"><span data-stu-id="a9fd2-170">Request body property</span></span>    | <span data-ttu-id="a9fd2-171">Description</span><span class="sxs-lookup"><span data-stu-id="a9fd2-171">Description</span></span>
    ---|---
    <span data-ttu-id="a9fd2-172">Id</span><span class="sxs-lookup"><span data-stu-id="a9fd2-172">Id</span></span> | <span data-ttu-id="a9fd2-173">The ContentKey ID is generated using the following format, “nb:kid:UUID:<NEW GUID>”.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-173">The ContentKey ID is generated using the following format, “nb:kid:UUID:<NEW GUID>”.</span></span>
    <span data-ttu-id="a9fd2-174">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="a9fd2-174">ContentKeyType</span></span> | <span data-ttu-id="a9fd2-175">The content key type is an integer that defines the key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-175">The content key type is an integer that defines the key.</span></span> <span data-ttu-id="a9fd2-176">For storage encryption format, the value is 1.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-176">For storage encryption format, the value is 1.</span></span>
    <span data-ttu-id="a9fd2-177">EncryptedContentKey</span><span class="sxs-lookup"><span data-stu-id="a9fd2-177">EncryptedContentKey</span></span> | <span data-ttu-id="a9fd2-178">We create a new content key value that is a 256-bit (32 bytes) value.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-178">We create a new content key value that is a 256-bit (32 bytes) value.</span></span> <span data-ttu-id="a9fd2-179">The key is encrypted using the storage encryption X.509 certificate that we retrieve from Microsoft Azure Media Services by executing an HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-179">The key is encrypted using the storage encryption X.509 certificate that we retrieve from Microsoft Azure Media Services by executing an HTTP GET request for the GetProtectionKeyId and GetProtectionKey Methods.</span></span> <span data-ttu-id="a9fd2-180">As an example, see the following .NET code: the  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span><span class="sxs-lookup"><span data-stu-id="a9fd2-180">As an example, see the following .NET code: the  **EncryptSymmetricKeyData** method defined [here](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.FileEncryption/EncryptionUtils.cs).</span></span>
    <span data-ttu-id="a9fd2-181">ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="a9fd2-181">ProtectionKeyId</span></span> | <span data-ttu-id="a9fd2-182">This is the protection key ID for the storage encryption X.509 certificate that was used to encrypt our content key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-182">This is the protection key ID for the storage encryption X.509 certificate that was used to encrypt our content key.</span></span>
    <span data-ttu-id="a9fd2-183">ProtectionKeyType</span><span class="sxs-lookup"><span data-stu-id="a9fd2-183">ProtectionKeyType</span></span> | <span data-ttu-id="a9fd2-184">This is the encryption type for the protection key that was used to encrypt the content key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-184">This is the encryption type for the protection key that was used to encrypt the content key.</span></span> <span data-ttu-id="a9fd2-185">This value is StorageEncryption(1) for our example.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-185">This value is StorageEncryption(1) for our example.</span></span>
    <span data-ttu-id="a9fd2-186">Checksum</span><span class="sxs-lookup"><span data-stu-id="a9fd2-186">Checksum</span></span> |<span data-ttu-id="a9fd2-187">The MD5 calculated checksum for the content key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-187">The MD5 calculated checksum for the content key.</span></span> <span data-ttu-id="a9fd2-188">It is computed by encrypting the content ID with the content key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-188">It is computed by encrypting the content ID with the content key.</span></span> <span data-ttu-id="a9fd2-189">The example code demonstrates how to calculate the checksum.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-189">The example code demonstrates how to calculate the checksum.</span></span>


### <a name="retrieve-the-protectionkeyid"></a><span data-ttu-id="a9fd2-190">Retrieve the ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="a9fd2-190">Retrieve the ProtectionKeyId</span></span>
<span data-ttu-id="a9fd2-191">The following example shows how to retrieve the ProtectionKeyId, a certificate thumbprint, for the certificate you must use when encrypting your content key.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-191">The following example shows how to retrieve the ProtectionKeyId, a certificate thumbprint, for the certificate you must use when encrypting your content key.</span></span> <span data-ttu-id="a9fd2-192">Do this step to make sure that you already have the appropriate certificate on your machine.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-192">Do this step to make sure that you already have the appropriate certificate on your machine.</span></span>

<span data-ttu-id="a9fd2-193">Request:</span><span class="sxs-lookup"><span data-stu-id="a9fd2-193">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKeyId?contentKeyType=0 HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.17
    Host: media.windows.net

<span data-ttu-id="a9fd2-194">Response:</span><span class="sxs-lookup"><span data-stu-id="a9fd2-194">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 139
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    x-ms-request-id: 2b6aa7a4-3a09-4b08-b581-26b55667f817
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:42:52 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String","value":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C"}

### <a name="retrieve-the-protectionkey-for-the-protectionkeyid"></a><span data-ttu-id="a9fd2-195">Retrieve the ProtectionKey for the ProtectionKeyId</span><span class="sxs-lookup"><span data-stu-id="a9fd2-195">Retrieve the ProtectionKey for the ProtectionKeyId</span></span>
<span data-ttu-id="a9fd2-196">The following example shows how to retrieve the X.509 certificate using the ProtectionKeyId you received in the previous step.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-196">The following example shows how to retrieve the X.509 certificate using the ProtectionKeyId you received in the previous step.</span></span>

<span data-ttu-id="a9fd2-197">Request:</span><span class="sxs-lookup"><span data-stu-id="a9fd2-197">Request:</span></span>

    GET https://media.windows.net/api/GetProtectionKey?ProtectionKeyId='7D9BB04D9D0A4A24800CADBFEF232689E048F69C' HTTP/1.1
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-e769-2233-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.17
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    Host: media.windows.net

<span data-ttu-id="a9fd2-198">Response:</span><span class="sxs-lookup"><span data-stu-id="a9fd2-198">Response:</span></span>

    HTTP/1.1 200 OK
    Cache-Control: no-cache
    Content-Length: 1227
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: 78d1247a-58d7-40e5-96cc-70ff0dfa7382
    request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    x-ms-request-id: 1523e8f3-8ed2-40fe-8a9a-5d81eb572cc8
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Thu, 05 Feb 2015 07:52:30 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Edm.String",
    "value":"MIIDSTCCAjGgAwIBAgIQqf92wku/HLJGCbMAU8GEnDANBgkqhkiG9w0BAQQFADAuMSwwKgYDVQQDEyN3YW1zYmx1cmVnMDAxZW5jcnlwdGFsbHNlY3JldHMtY2VydDAeFw0xMjA1MjkwNzAwMDBaFw0zMjA1MjkwNzAwMDBaMC4xLDAqBgNVBAMTI3dhbXNibHVyZWcwMDFlbmNyeXB0YWxsc2VjcmV0cy1jZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAzR0SEbXefvUjb9wCUfkEiKtGQ5Gc328qFPrhMjSo+YHe0AVviZ9YaxPPb0m1AaaRV4dqWpST2+JtDhLOmGpWmmA60tbATJDdmRzKi2eYAyhhE76MgJgL3myCQLP42jDusWXWSMabui3/tMDQs+zfi1sJ4Ch/lm5EvksYsu6o8sCv29VRwxfDLJPBy2NlbV4GbWz5Qxp2tAmHoROnfaRhwp6WIbquk69tEtu2U50CpPN2goLAqx2PpXAqA+prxCZYGTHqfmFJEKtZHhizVBTFPGS3ncfnQC9QIEwFbPw6E5PO5yNaB68radWsp5uvDg33G1i8IT39GstMW6zaaG7cNQIDAQABo2MwYTBfBgNVHQEEWDBWgBCOGT2hPhsvQioZimw8M+jOoTAwLjEsMCoGA1UEAxMjd2Ftc2JsdXJlZzAwMWVuY3J5cHRhbGxzZWNyZXRzLWNlcnSCEKn/dsJLvxyyRgmzAFPBhJwwDQYJKoZIhvcNAQEEBQADggEBABcrQPma2ekNS3Wc5wGXL/aHyQaQRwFGymnUJ+VR8jVUZaC/U/f6lR98eTlwycjVwRL7D15BfClGEHw66QdHejaViJCjbEIJJ3p2c9fzBKhjLhzB3VVNiLIaH6RSI1bMPd2eddSCqhDIn3VBN605GcYXMzhYp+YA6g9+YMNeS1b+LxX3fqixMQIxSHOLFZ1G/H2xfNawv0VikH3djNui3EKT1w/8aRkUv/AAV0b3rYkP/jA1I0CPn0XFk7STYoiJ3gJoKq9EMXhit+Iwfz0sMkfhWG12/XO+TAWqsK1ZxEjuC9OzrY7pFnNxs4Mu4S8iinehduSpY+9mDd3dHynNwT4="}

### <a name="create-the-content-key"></a><span data-ttu-id="a9fd2-199">Create the content key</span><span class="sxs-lookup"><span data-stu-id="a9fd2-199">Create the content key</span></span>
<span data-ttu-id="a9fd2-200">After you have retrieved the X.509 certificate and used its public key to encrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-200">After you have retrieved the X.509 certificate and used its public key to encrypt your content key, create a **ContentKey** entity and set its property values accordingly.</span></span>

<span data-ttu-id="a9fd2-201">One of the values that you must set when create the content key is the type.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-201">One of the values that you must set when create the content key is the type.</span></span> <span data-ttu-id="a9fd2-202">When using storage encryption, the value should be set to '1'.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-202">When using storage encryption, the value should be set to '1'.</span></span> 

<span data-ttu-id="a9fd2-203">The following example shows how to create a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and the **ProtectionKeyType** set to "0" to indicate that the protection key ID is the X.509 certificate thumbprint.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-203">The following example shows how to create a **ContentKey** with a **ContentKeyType** set for storage encryption ("1") and the **ProtectionKeyType** set to "0" to indicate that the protection key ID is the X.509 certificate thumbprint.</span></span>  

<span data-ttu-id="a9fd2-204">Request</span><span class="sxs-lookup"><span data-stu-id="a9fd2-204">Request</span></span>

    POST https://media.windows.net/api/ContentKeys HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423034908&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=7eSLe1GHnxgilr3F2FPCGxdL2%2bwy%2f39XhMPGY9IizfU%3d
    x-ms-version: 2.17
    Host: media.windows.net
    {
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C", 
    "ContentKeyType":"1", 
    "ProtectionKeyType":"0",
    "EncryptedContentKey":"your encrypted content key",
    "Checksum":"calculated checksum"
    }

<span data-ttu-id="a9fd2-205">Response:</span><span class="sxs-lookup"><span data-stu-id="a9fd2-205">Response:</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 777
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://media.windows.net/api/ContentKeys('nb%3Akid%3AUUID%3A9c8ea9c6-52bd-4232-8a43-8e43d8564a99')
    Server: Microsoft-IIS/8.5
    request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    x-ms-request-id: 76e85e0f-5cf1-44cb-b689-b3455888682c
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Wed, 04 Feb 2015 02:37:46 GMT

    {"odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#ContentKeys/@Element",
    "Id":"nb:kid:UUID:9c8ea9c6-52bd-4232-8a43-8e43d8564a99","Created":"2015-02-04T02:37:46.9684379Z",
    "LastModified":"2015-02-04T02:37:46.9684379Z",
    "ContentKeyType":1,
    "EncryptedContentKey":"your encrypted content key",
    "Name":"ContentKey",
    "ProtectionKeyId":"7D9BB04D9D0A4A24800CADBFEF232689E048F69C",
    "ProtectionKeyType":0,
    "Checksum":"calculated checksum"}

## <a name="create-an-asset"></a><span data-ttu-id="a9fd2-206">Create an asset</span><span class="sxs-lookup"><span data-stu-id="a9fd2-206">Create an asset</span></span>
<span data-ttu-id="a9fd2-207">The following example shows how to create an asset.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-207">The following example shows how to create an asset.</span></span>

<span data-ttu-id="a9fd2-208">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a9fd2-208">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Assets HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-2233-b1ae-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.17
    Host: media.windows.net

    {"Name":"BigBuckBunny" "Options":1}

<span data-ttu-id="a9fd2-209">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a9fd2-209">**HTTP Response**</span></span>

<span data-ttu-id="a9fd2-210">If successful, the following response is returned:</span><span class="sxs-lookup"><span data-stu-id="a9fd2-210">If successful, the following response is returned:</span></span>

    HTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 452
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1')
    Server: Microsoft-IIS/8.5
    x-ms-client-request-id: c59de965-bc89-4295-9a57-75d897e5221e
    request-id: e98be122-ae09-473a-8072-0ccd234a0657
    x-ms-request-id: e98be122-ae09-473a-8072-0ccd234a0657
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Sun, 18 Jan 2015 22:06:40 GMT
    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Assets/@Element",
       "Id":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "State":0,
       "Created":"2015-01-18T22:06:40.6010903Z",
       "LastModified":"2015-01-18T22:06:40.6010903Z",
       "AlternateId":null,
       "Name":"BigBuckBunny.mp4",
       "Options":1,
       "Uri":"https://storagetestaccount001.blob.core.windows.net/asset-9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "StorageAccountName":"storagetestaccount001"
    }

## <a name="associate-the-contentkey-with-an-asset"></a><span data-ttu-id="a9fd2-211">Associate the ContentKey with an Asset</span><span class="sxs-lookup"><span data-stu-id="a9fd2-211">Associate the ContentKey with an Asset</span></span>
<span data-ttu-id="a9fd2-212">After creating the ContentKey, associate it with your Asset using the $links operation, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="a9fd2-212">After creating the ContentKey, associate it with your Asset using the $links operation, as shown in the following example:</span></span>

<span data-ttu-id="a9fd2-213">Request:</span><span class="sxs-lookup"><span data-stu-id="a9fd2-213">Request:</span></span>

    POST https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Afbd7ce05-1087-401b-aaae-29f16383c801')/$links/ContentKeys HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Content-Type: application/json
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=juliakoams1&urn%3aSubscriptionId=zbbef702-2233-477b-9f16-bc4d3aa97387&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1423141026&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=lDBz5YXKiWe5L7eXOHsLHc9kKEUcUiFJvrNFFSksgkM%3d
    x-ms-version: 2.17
    Host: media.windows.net

    {"uri":"https://wamsbayclus001rest-hs.cloudapp.net/api/ContentKeys('nb%3Akid%3AUUID%3A01e6ea36-2285-4562-91f1-82c45736047c')"}

<span data-ttu-id="a9fd2-214">Response:</span><span class="sxs-lookup"><span data-stu-id="a9fd2-214">Response:</span></span>

    HTTP/1.1 204 No Content 

## <a name="create-an-assetfile"></a><span data-ttu-id="a9fd2-215">Create an AssetFile</span><span class="sxs-lookup"><span data-stu-id="a9fd2-215">Create an AssetFile</span></span>
<span data-ttu-id="a9fd2-216">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-216">The [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) entity represents a video or audio file that is stored in a blob container.</span></span> <span data-ttu-id="a9fd2-217">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-217">An asset file is always associated with an asset, and an asset may contain one or many asset files.</span></span> <span data-ttu-id="a9fd2-218">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-218">The Media Services Encoder task fails if an asset file object is not associated with a digital file in a blob container.</span></span>

<span data-ttu-id="a9fd2-219">The **AssetFile** instance and the actual media file are two distinct objects.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-219">The **AssetFile** instance and the actual media file are two distinct objects.</span></span> <span data-ttu-id="a9fd2-220">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span><span class="sxs-lookup"><span data-stu-id="a9fd2-220">The AssetFile instance contains metadata about the media file, while the media file contains the actual media content.</span></span>

<span data-ttu-id="a9fd2-221">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (not shown in this article).</span><span class="sxs-lookup"><span data-stu-id="a9fd2-221">After you upload your digital media file into a blob container, you will use the **MERGE** HTTP request to update the AssetFile with information about your media file (not shown in this article).</span></span> 

<span data-ttu-id="a9fd2-222">**HTTP Request**</span><span class="sxs-lookup"><span data-stu-id="a9fd2-222">**HTTP Request**</span></span>

    POST https://media.windows.net/api/Files HTTP/1.1
    Content-Type: application/json
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    Authorization: Bearer http%3a%2f%2fschemas.xmlsoap.org%2fws%2f2005%2f05%2fidentity%2fclaims%2fnameidentifier=amstestaccount001&urn%3aSubscriptionId=z7f09258-6753-4ca2-2233-193798e2c9d8&http%3a%2f%2fschemas.microsoft.com%2faccesscontrolservice%2f2010%2f07%2fclaims%2fidentityprovider=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&Audience=urn%3aWindowsAzureMediaServices&ExpiresOn=1421640053&Issuer=https%3a%2f%2fwamsprodglobal001acs.accesscontrol.windows.net%2f&HMACSHA256=vlG%2fPYdFDMS1zKc36qcFVWnaNh07UCkhYj3B71%2fk1YA%3d
    x-ms-version: 2.17
    Host: media.windows.net
    Content-Length: 164

    {  
       "IsEncrypted":"true",
       "EncryptionScheme" : "StorageEncryption", 
       "EncryptionVersion" : "1.0",       
       "EncryptionKeyId" : "nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector" : "397304628502661816</d:InitializationVector",
       "Options":0,
       "IsPrimary":"false",
       "MimeType":"video/mp4",
       "Name":"BigBuckBunny.mp4",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1"
    }

<span data-ttu-id="a9fd2-223">**HTTP Response**</span><span class="sxs-lookup"><span data-stu-id="a9fd2-223">**HTTP Response**</span></span>

    HTTP/1.1 201 Created
    Cache-Control: no-cache
    Content-Length: 535
    Content-Type: application/json;odata=minimalmetadata;streaming=true;charset=utf-8
    Location: https://wamsbayclus001rest-hs.cloudapp.net/api/Files('nb%3Acid%3AUUID%3Af13a0137-0a62-9d4c-b3b9-ca944b5142c5')
    Server: Microsoft-IIS/8.5
    request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    x-ms-request-id: 98a30e2d-f379-4495-988e-0b79edc9b80e
    X-Content-Type-Options: nosniff
    DataServiceVersion: 3.0;
    X-Powered-By: ASP.NET
    Strict-Transport-Security: max-age=31536000; includeSubDomains
    Date: Mon, 19 Jan 2015 00:34:07 GMT

    {  
       "odata.metadata":"https://wamsbayclus001rest-hs.cloudapp.net/api/$metadata#Files/@Element",
       "Id":"nb:cid:UUID:f13a0137-0a62-9d4c-b3b9-ca944b5142c5",
       "Name":"BigBuckBunny.mp4",
       "ContentFileSize":"0",
       "ParentAssetId":"nb:cid:UUID:9bc8ff20-24fb-4fdb-9d7c-b04c7ee573a1",
       "EncryptionVersion": "1.0",
       "EncryptionScheme": "StorageEncryption",
       "IsEncrypted":true,
       "EncryptionKeyId":"nb:kid:UUID:32e6efaf-5fba-4538-b115-9d1cefe43510",
       "InitializationVector":"397304628502661816</d:InitializationVector",
       "IsPrimary":false,
       "LastModified":"2015-01-19T00:34:08.1934137Z",
       "Created":"2015-01-19T00:34:08.1934137Z",
       "MimeType":"video/mp4",
       "ContentChecksum":null
    }
