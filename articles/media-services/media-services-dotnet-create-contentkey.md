---
title: Create ContentKeys with .NET
description: Learn how to create content keys that provide secure access to Assets.
services: media-services
documentationcenter: ''
author: Juliako
manager: erikre
editor: ''
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: c547afd9535eb4764caf6b37d4e38a22f6e88186
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549087"
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="aff87-103">Create ContentKeys with .NET</span><span class="sxs-lookup"><span data-stu-id="aff87-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [REST](media-services-rest-create-contentkey.md)
> * [.NET](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="aff87-106">Media Services enables you to create and deliver encrypted assets.</span><span class="sxs-lookup"><span data-stu-id="aff87-106">Media Services enables you to create and deliver encrypted assets.</span></span> <span data-ttu-id="aff87-107">A **ContentKey** provides secure access to your **Asset**s.</span><span class="sxs-lookup"><span data-stu-id="aff87-107">A **ContentKey** provides secure access to your **Asset**s.</span></span> 

<span data-ttu-id="aff87-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="aff87-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="aff87-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="aff87-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="aff87-110">Encrypted assets have to be associated with **ContentKey**s.</span><span class="sxs-lookup"><span data-stu-id="aff87-110">Encrypted assets have to be associated with **ContentKey**s.</span></span> <span data-ttu-id="aff87-111">This article describes how to create a content key.</span><span class="sxs-lookup"><span data-stu-id="aff87-111">This article describes how to create a content key.</span></span>

> [!NOTE]
> When creating a new **StorageEncrypted** asset using the Media Services .NET SDK , the **ContentKey** is automatically created and linked with the asset.
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="aff87-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="aff87-113">ContentKeyType</span></span>
<span data-ttu-id="aff87-114">One of the values that you must set when create a content key is the content key type.</span><span class="sxs-lookup"><span data-stu-id="aff87-114">One of the values that you must set when create a content key is the content key type.</span></span> <span data-ttu-id="aff87-115">Choose from one of the following values.</span><span class="sxs-lookup"><span data-stu-id="aff87-115">Choose from one of the following values.</span></span> 

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

## <a id="envelope_contentkey"></a><span data-ttu-id="aff87-116">Create envelope type ContentKey</span><span class="sxs-lookup"><span data-stu-id="aff87-116">Create envelope type ContentKey</span></span>
<span data-ttu-id="aff87-117">The following code snippet creates a content key of the envelope encryption type.</span><span class="sxs-lookup"><span data-stu-id="aff87-117">The following code snippet creates a content key of the envelope encryption type.</span></span> <span data-ttu-id="aff87-118">It then associates the key with the specified asset.</span><span class="sxs-lookup"><span data-stu-id="aff87-118">It then associates the key with the specified asset.</span></span>

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

<span data-ttu-id="aff87-119">call</span><span class="sxs-lookup"><span data-stu-id="aff87-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <a id="common_contentkey"></a><span data-ttu-id="aff87-120">Create common type ContentKey</span><span class="sxs-lookup"><span data-stu-id="aff87-120">Create common type ContentKey</span></span>
<span data-ttu-id="aff87-121">The following code snippet creates a content key of the common encryption type.</span><span class="sxs-lookup"><span data-stu-id="aff87-121">The following code snippet creates a content key of the common encryption type.</span></span> <span data-ttu-id="aff87-122">It then associates the key with the specified asset.</span><span class="sxs-lookup"><span data-stu-id="aff87-122">It then associates the key with the specified asset.</span></span>

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
<span data-ttu-id="aff87-123">call</span><span class="sxs-lookup"><span data-stu-id="aff87-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="aff87-124">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="aff87-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="aff87-125">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="aff87-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

