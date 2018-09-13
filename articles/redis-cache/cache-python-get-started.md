---
title: How to use Azure Redis Cache with Python | Microsoft Docs
description: Get started with Azure Redis Cache using Python
services: redis-cache
documentationcenter: ''
author: steved0x
manager: douge
editor: v-lincan
ms.assetid: f186202c-fdad-4398-af8c-aee91ec96ba3
ms.service: cache
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/10/2017
ms.author: sdanie
ms.openlocfilehash: cdbee52574d0ffbe82ef3dc98f2848f4d00ba2ff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554374"
---
# <a name="how-to-use-azure-redis-cache-with-python"></a><span data-ttu-id="a05f3-103">How to use Azure Redis Cache with Python</span><span class="sxs-lookup"><span data-stu-id="a05f3-103">How to use Azure Redis Cache with Python</span></span>
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

<span data-ttu-id="a05f3-109">This topic shows you how to get started with Azure Redis Cache using Python.</span><span class="sxs-lookup"><span data-stu-id="a05f3-109">This topic shows you how to get started with Azure Redis Cache using Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a05f3-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a05f3-110">Prerequisites</span></span>
<span data-ttu-id="a05f3-111">Install [redis-py](https://github.com/andymccurdy/redis-py).</span><span class="sxs-lookup"><span data-stu-id="a05f3-111">Install [redis-py](https://github.com/andymccurdy/redis-py).</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="a05f3-112">Create a Redis cache on Azure</span><span class="sxs-lookup"><span data-stu-id="a05f3-112">Create a Redis cache on Azure</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

## <a name="retrieve-the-host-name-and-access-keys"></a><span data-ttu-id="a05f3-113">Retrieve the host name and access keys</span><span class="sxs-lookup"><span data-stu-id="a05f3-113">Retrieve the host name and access keys</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

## <a name="enable-the-non-ssl-endpoint"></a><span data-ttu-id="a05f3-114">Enable the non-SSL endpoint</span><span class="sxs-lookup"><span data-stu-id="a05f3-114">Enable the non-SSL endpoint</span></span>
<span data-ttu-id="a05f3-115">Some Redis clients don't support SSL, and by default the [non-SSL port is disabled for new Azure Redis Cache instances](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="a05f3-115">Some Redis clients don't support SSL, and by default the [non-SSL port is disabled for new Azure Redis Cache instances](cache-configure.md#access-ports).</span></span> <span data-ttu-id="a05f3-116">At the time of this writing, the [redis-py](https://github.com/andymccurdy/redis-py) client doesn't support SSL.</span><span class="sxs-lookup"><span data-stu-id="a05f3-116">At the time of this writing, the [redis-py](https://github.com/andymccurdy/redis-py) client doesn't support SSL.</span></span> 

[!INCLUDE [redis-cache-create](../../includes/redis-cache-non-ssl-port.md)]

## <a name="add-something-to-the-cache-and-retrieve-it"></a><span data-ttu-id="a05f3-117">Add something to the cache and retrieve it</span><span class="sxs-lookup"><span data-stu-id="a05f3-117">Add something to the cache and retrieve it</span></span>
    >>> import redis
    >>> r = redis.StrictRedis(host='<name>.redis.cache.windows.net',
          port=6380, db=0, password='<key>', ssl=True)
    >>> r.set('foo', 'bar')
    True
    >>> r.get('foo')
    b'bar'


<span data-ttu-id="a05f3-118">Replace `<name>` with your cache name and `key` with your access key.</span><span class="sxs-lookup"><span data-stu-id="a05f3-118">Replace `<name>` with your cache name and `key` with your access key.</span></span>

<!--Image references-->
[1]: ./media/cache-python-get-started/redis-cache-new-cache-menu.png
[2]: ./media/cache-python-get-started/redis-cache-cache-create.png
