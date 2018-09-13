---
title: Pass authentication tokens to Azure Media Services | Microsoft Docs
description: Learn how to send authentication tokens from the client to the Azure Media Services key delivery service
services: media-services
keywords: content protection, DRM, token authentication
documentationcenter: ''
author: dbgeorge
manager: jasonsue
editor: ''
ms.assetid: 7c3b35d9-1269-4c83-8c91-490ae65b0817
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2017
ms.author: dwgeo
ms.openlocfilehash: b6aca2928465b73e35ac15f01bb776b1f69add0b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968610"
---
# <a name="learn-how-clients-pass-tokens-to-the-azure-media-services-key-delivery-service"></a><span data-ttu-id="8bddf-104">Learn how clients pass tokens to the Azure Media Services key delivery service</span><span class="sxs-lookup"><span data-stu-id="8bddf-104">Learn how clients pass tokens to the Azure Media Services key delivery service</span></span>
<span data-ttu-id="8bddf-105">Customers often ask how a player can pass tokens to the Azure Media Services key delivery service for verification so the player can obtain the key.</span><span class="sxs-lookup"><span data-stu-id="8bddf-105">Customers often ask how a player can pass tokens to the Azure Media Services key delivery service for verification so the player can obtain the key.</span></span> <span data-ttu-id="8bddf-106">Media Services supports the simple web token (SWT) and JSON Web Token (JWT) formats.</span><span class="sxs-lookup"><span data-stu-id="8bddf-106">Media Services supports the simple web token (SWT) and JSON Web Token (JWT) formats.</span></span> <span data-ttu-id="8bddf-107">Token authentication is applied to any type of key, regardless of whether you use common encryption or Advanced Encryption Standard (AES) envelope encryption in the system.</span><span class="sxs-lookup"><span data-stu-id="8bddf-107">Token authentication is applied to any type of key, regardless of whether you use common encryption or Advanced Encryption Standard (AES) envelope encryption in the system.</span></span>

 <span data-ttu-id="8bddf-108">Depending on the player and platform you target, you can pass the token with your player in the following ways:</span><span class="sxs-lookup"><span data-stu-id="8bddf-108">Depending on the player and platform you target, you can pass the token with your player in the following ways:</span></span>

- <span data-ttu-id="8bddf-109">Through the HTTP Authorization header.</span><span class="sxs-lookup"><span data-stu-id="8bddf-109">Through the HTTP Authorization header.</span></span>
    > [!NOTE]
    > <span data-ttu-id="8bddf-110">The "Bearer" prefix is expected per the OAuth 2.0 specs.</span><span class="sxs-lookup"><span data-stu-id="8bddf-110">The "Bearer" prefix is expected per the OAuth 2.0 specs.</span></span> <span data-ttu-id="8bddf-111">A sample player with the token configuration is hosted on the Azure Media Player [demo page](http://ampdemo.azureedge.net/).</span><span class="sxs-lookup"><span data-stu-id="8bddf-111">A sample player with the token configuration is hosted on the Azure Media Player [demo page](http://ampdemo.azureedge.net/).</span></span> <span data-ttu-id="8bddf-112">To set the video source, choose **AES (JWT Token)** or **AES (SWT Token)**.</span><span class="sxs-lookup"><span data-stu-id="8bddf-112">To set the video source, choose **AES (JWT Token)** or **AES (SWT Token)**.</span></span> <span data-ttu-id="8bddf-113">The token is passed via the Authorization header.</span><span class="sxs-lookup"><span data-stu-id="8bddf-113">The token is passed via the Authorization header.</span></span>

- <span data-ttu-id="8bddf-114">Via the addition of a URL query parameter with "token=tokenvalue."</span><span class="sxs-lookup"><span data-stu-id="8bddf-114">Via the addition of a URL query parameter with "token=tokenvalue."</span></span>  
    > [!NOTE]
    > <span data-ttu-id="8bddf-115">The "Bearer" prefix isn't expected.</span><span class="sxs-lookup"><span data-stu-id="8bddf-115">The "Bearer" prefix isn't expected.</span></span> <span data-ttu-id="8bddf-116">Because the token is sent through a URL, you need to armor the token string.</span><span class="sxs-lookup"><span data-stu-id="8bddf-116">Because the token is sent through a URL, you need to armor the token string.</span></span> <span data-ttu-id="8bddf-117">Here is a C# sample code that shows how to do it:</span><span class="sxs-lookup"><span data-stu-id="8bddf-117">Here is a C# sample code that shows how to do it:</span></span>

    ```csharp
    string armoredAuthToken = System.Web.HttpUtility.UrlEncode(authToken);
    string uriWithTokenParameter = string.Format("{0}&token={1}", keyDeliveryServiceUri.AbsoluteUri, armoredAuthToken);
    Uri keyDeliveryUrlWithTokenParameter = new Uri(uriWithTokenParameter);
    ```

- <span data-ttu-id="8bddf-118">Through the CustomData field.</span><span class="sxs-lookup"><span data-stu-id="8bddf-118">Through the CustomData field.</span></span>
<span data-ttu-id="8bddf-119">This option is used for PlayReady license acquisition only, through the CustomData field of the PlayReady License Acquisition Challenge.</span><span class="sxs-lookup"><span data-stu-id="8bddf-119">This option is used for PlayReady license acquisition only, through the CustomData field of the PlayReady License Acquisition Challenge.</span></span> <span data-ttu-id="8bddf-120">In this case, the token must be inside the XML document as described here:</span><span class="sxs-lookup"><span data-stu-id="8bddf-120">In this case, the token must be inside the XML document as described here:</span></span>

    ```xml
    <?xml version="1.0"?>
    <CustomData xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyCustomData/v1"> 
        <Token></Token> 
    </CustomData>
    ```
    <span data-ttu-id="8bddf-121">Put your authentication token in the Token element.</span><span class="sxs-lookup"><span data-stu-id="8bddf-121">Put your authentication token in the Token element.</span></span>

- <span data-ttu-id="8bddf-122">Through an alternate HTTP Live Streaming (HLS) playlist.</span><span class="sxs-lookup"><span data-stu-id="8bddf-122">Through an alternate HTTP Live Streaming (HLS) playlist.</span></span> <span data-ttu-id="8bddf-123">If you need to configure token authentication for AES + HLS playback on iOS/Safari, there isn't a way you can directly send in the token.</span><span class="sxs-lookup"><span data-stu-id="8bddf-123">If you need to configure token authentication for AES + HLS playback on iOS/Safari, there isn't a way you can directly send in the token.</span></span> <span data-ttu-id="8bddf-124">For more information on how to alternate the playlist to enable this scenario, see this [blog post](http://azure.microsoft.com/blog/2015/03/06/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span><span class="sxs-lookup"><span data-stu-id="8bddf-124">For more information on how to alternate the playlist to enable this scenario, see this [blog post](http://azure.microsoft.com/blog/2015/03/06/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bddf-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="8bddf-125">Next steps</span></span>

[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]