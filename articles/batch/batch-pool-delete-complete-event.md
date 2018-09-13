---
title: Pool delete complete event - Azure | Microsoft Docs
ms.custom: ''
ms.date: 2017-02-01
ms.prod: azure
ms.reviewer: ''
ms.service: batch
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 580a1278-5740-4143-826c-7d875ef127ff
caps.latest.revision: 5
author: tamram
ms.author: tamram
manager: timlt
ms.openlocfilehash: 0710d5762f0e68380a531f94baa88a8007565912
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563680"
---
# <a name="pool-delete-complete-event"></a><span data-ttu-id="30c18-102">Pool delete complete event</span><span class="sxs-lookup"><span data-stu-id="30c18-102">Pool delete complete event</span></span>

 <span data-ttu-id="30c18-103">This event is emitted when a pool delete operation has completed.</span><span class="sxs-lookup"><span data-stu-id="30c18-103">This event is emitted when a pool delete operation has completed.</span></span>

 <span data-ttu-id="30c18-104">The following example shows the body of a pool delete complete event.</span><span class="sxs-lookup"><span data-stu-id="30c18-104">The following example shows the body of a pool delete complete event.</span></span>

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|<span data-ttu-id="30c18-105">Element</span><span class="sxs-lookup"><span data-stu-id="30c18-105">Element</span></span>|<span data-ttu-id="30c18-106">Type</span><span class="sxs-lookup"><span data-stu-id="30c18-106">Type</span></span>|<span data-ttu-id="30c18-107">Notes</span><span class="sxs-lookup"><span data-stu-id="30c18-107">Notes</span></span>|
|-------------|----------|-----------|
|<span data-ttu-id="30c18-108">id</span><span class="sxs-lookup"><span data-stu-id="30c18-108">id</span></span>|<span data-ttu-id="30c18-109">String</span><span class="sxs-lookup"><span data-stu-id="30c18-109">String</span></span>|<span data-ttu-id="30c18-110">The id of the pool.</span><span class="sxs-lookup"><span data-stu-id="30c18-110">The id of the pool.</span></span>|
|<span data-ttu-id="30c18-111">startTime</span><span class="sxs-lookup"><span data-stu-id="30c18-111">startTime</span></span>|<span data-ttu-id="30c18-112">DateTime</span><span class="sxs-lookup"><span data-stu-id="30c18-112">DateTime</span></span>|<span data-ttu-id="30c18-113">The time the pool delete started.</span><span class="sxs-lookup"><span data-stu-id="30c18-113">The time the pool delete started.</span></span>|
|<span data-ttu-id="30c18-114">endTime</span><span class="sxs-lookup"><span data-stu-id="30c18-114">endTime</span></span>|<span data-ttu-id="30c18-115">DateTime</span><span class="sxs-lookup"><span data-stu-id="30c18-115">DateTime</span></span>|<span data-ttu-id="30c18-116">The time the pool delete completed.</span><span class="sxs-lookup"><span data-stu-id="30c18-116">The time the pool delete completed.</span></span>|

## <a name="remarks"></a><span data-ttu-id="30c18-117">Remarks</span><span class="sxs-lookup"><span data-stu-id="30c18-117">Remarks</span></span>
<span data-ttu-id="30c18-118">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span><span class="sxs-lookup"><span data-stu-id="30c18-118">For more information about states and error codes for pool resize operation, see [Delete a pool from an account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).</span></span>