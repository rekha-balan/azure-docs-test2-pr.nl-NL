---
title: Create ContentKeys with .NET
description: Learn how to create content keys that provide secure access to Assets.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 53df4c4cef19f6eef99aa15bb265317aa0cd1d58
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856404"
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="d9f25-103">Create ContentKeys with .NET</span><span class="sxs-lookup"><span data-stu-id="d9f25-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [REST](media-services-rest-create-contentkey.md)
> * [.NET](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="d9f25-106">Media Services enables you to create and deliver encrypted assets.</span><span class="sxs-lookup"><span data-stu-id="d9f25-106">Media Services enables you to create and deliver encrypted assets.</span></span> <span data-ttu-id="d9f25-107">A **ContentKey** provides secure access to your **Asset**s.</span><span class="sxs-lookup"><span data-stu-id="d9f25-107">A **ContentKey** provides secure access to your **Asset**s.</span></span> 

<span data-ttu-id="d9f25-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="d9f25-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="d9f25-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="d9f25-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="d9f25-110">Encrypted assets have to be associated with **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="d9f25-110">Encrypted assets have to be associated with **ContentKey**s.</span></span> <span data-ttu-id="d9f25-111">This article describes how to create a content key.</span><span class="sxs-lookup"><span data-stu-id="d9f25-111">This article describes how to create a content key.</span></span>

> [!NOTE]
> When creating a new **StorageEncrypted** asset using the Media Services .NET SDK , the **ContentKey** is automatically created and linked with the asset.
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="d9f25-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="d9f25-113">ContentKeyType</span></span>
<span data-ttu-id="d9f25-114">One of the values that you must set when create a content key is the content key type.</span><span class="sxs-lookup"><span data-stu-id="d9f25-114">One of the values that you must set when create a content key is the content key type.</span></span> <span data-ttu-id="d9f25-115">Choose from one of the following values.</span><span class="sxs-lookup"><span data-stu-id="d9f25-115">Choose from one of the following values.</span></span> 

```csharp
    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is the default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }
```

## <a id="envelope_contentkey"></a><span data-ttu-id="d9f25-116">Create envelope type ContentKey</span><span class="sxs-lookup"><span data-stu-id="d9f25-116">Create envelope type ContentKey</span></span>
<span data-ttu-id="d9f25-117">The following code snippet creates a content key of the envelope encryption type.</span><span class="sxs-lookup"><span data-stu-id="d9f25-117">The following code snippet creates a content key of the envelope encryption type.</span></span> <span data-ttu-id="d9f25-118">It then associates the key with the specified asset.</span><span class="sxs-lookup"><span data-stu-id="d9f25-118">It then associates the key with the specified asset.</span></span>

```csharp
    static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
    {
        // Create envelope encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.EnvelopeEncryption);

        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int size)
    {
        byte[] randomBytes = new byte[size];
        using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
        {
            rng.GetBytes(randomBytes);
        }

        return randomBytes;
    }

call

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);
```


## <a id="common_contentkey"></a><span data-ttu-id="d9f25-119">Create common type ContentKey</span><span class="sxs-lookup"><span data-stu-id="d9f25-119">Create common type ContentKey</span></span>
<span data-ttu-id="d9f25-120">The following code snippet creates a content key of the common encryption type.</span><span class="sxs-lookup"><span data-stu-id="d9f25-120">The following code snippet creates a content key of the common encryption type.</span></span> <span data-ttu-id="d9f25-121">It then associates the key with the specified asset.</span><span class="sxs-lookup"><span data-stu-id="d9f25-121">It then associates the key with the specified asset.</span></span>

```csharp
    static public IContentKey CreateCommonTypeContentKey(IAsset asset)
    {
        // Create common encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.CommonEncryption);

        // Associate the key with the asset.
        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int length)
    {
        var returnValue = new byte[length];

        using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
        {
            rng.GetBytes(returnValue);
        }

        return returnValue;
    }
call

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 
```

## <a name="media-services-learning-paths"></a><span data-ttu-id="d9f25-122">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="d9f25-122">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d9f25-123">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="d9f25-123">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]
