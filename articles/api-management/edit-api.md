---
title: Edit an API with the Azure portal  | Microsoft Docs
description: This tutorial shows you how to use API Management (APIM) to edit an API.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 11/08/2017
ms.author: apimpm
ms.openlocfilehash: b39259fcfc93cb0a2a1a2dc600e5235da8cc6930
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868135"
---
# <a name="edit-an-api"></a><span data-ttu-id="3cdd2-103">Edit an API</span><span class="sxs-lookup"><span data-stu-id="3cdd2-103">Edit an API</span></span>

<span data-ttu-id="3cdd2-104">The steps in this tutorial show you how to use API Management (APIM) to edit an API.</span><span class="sxs-lookup"><span data-stu-id="3cdd2-104">The steps in this tutorial show you how to use API Management (APIM) to edit an API.</span></span> 

+ <span data-ttu-id="3cdd2-105">You can do it by adding, deleting, renaming operations in the APIM instance.</span><span class="sxs-lookup"><span data-stu-id="3cdd2-105">You can do it by adding, deleting, renaming operations in the APIM instance.</span></span> 
+ <span data-ttu-id="3cdd2-106">You can edit your API's swagger.</span><span class="sxs-lookup"><span data-stu-id="3cdd2-106">You can edit your API's swagger.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3cdd2-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3cdd2-107">Prerequisites</span></span>

+ [<span data-ttu-id="3cdd2-108">Create an Azure API Management instance</span><span class="sxs-lookup"><span data-stu-id="3cdd2-108">Create an Azure API Management instance</span></span>](get-started-create-service-instance.md)
+ [<span data-ttu-id="3cdd2-109">Import and publish your first API</span><span class="sxs-lookup"><span data-stu-id="3cdd2-109">Import and publish your first API</span></span>](import-and-publish.md)

[!INCLUDE [api-management-navigate-to-instance.md](../../includes/api-management-navigate-to-instance.md)]

## <a name="edit-an-api-in-apim"></a><span data-ttu-id="3cdd2-110">Edit an API in APIM</span><span class="sxs-lookup"><span data-stu-id="3cdd2-110">Edit an API in APIM</span></span>

![Edit an api](./media/edit-api/edit-api001.png)

1. <span data-ttu-id="3cdd2-112">Click the **APIs** tab.</span><span class="sxs-lookup"><span data-stu-id="3cdd2-112">Click the **APIs** tab.</span></span>
2. <span data-ttu-id="3cdd2-113">Select one of the APIs that you previously imported.</span><span class="sxs-lookup"><span data-stu-id="3cdd2-113">Select one of the APIs that you previously imported.</span></span>
3. <span data-ttu-id="3cdd2-114">Select the **Design** tab.</span><span class="sxs-lookup"><span data-stu-id="3cdd2-114">Select the **Design** tab.</span></span>
4. <span data-ttu-id="3cdd2-115">Select an operation, which you want to edit.</span><span class="sxs-lookup"><span data-stu-id="3cdd2-115">Select an operation, which you want to edit.</span></span>
5. <span data-ttu-id="3cdd2-116">To rename the operation, select a **pencil** in the **Frontend** window.</span><span class="sxs-lookup"><span data-stu-id="3cdd2-116">To rename the operation, select a **pencil** in the **Frontend** window.</span></span>

## <a name="update-the-swagger"></a><span data-ttu-id="3cdd2-117">Update the swagger</span><span class="sxs-lookup"><span data-stu-id="3cdd2-117">Update the swagger</span></span>

<span data-ttu-id="3cdd2-118">You can update your backbend API from the Azure portal by following these steps:</span><span class="sxs-lookup"><span data-stu-id="3cdd2-118">You can update your backbend API from the Azure portal by following these steps:</span></span>

1. <span data-ttu-id="3cdd2-119">Select **All operations**</span><span class="sxs-lookup"><span data-stu-id="3cdd2-119">Select **All operations**</span></span>
2. <span data-ttu-id="3cdd2-120">Click pencil in the **Frontend** window.</span><span class="sxs-lookup"><span data-stu-id="3cdd2-120">Click pencil in the **Frontend** window.</span></span>

    ![Edit an api](./media/edit-api/edit-api002.png)

    <span data-ttu-id="3cdd2-122">Your API's swagger appears.</span><span class="sxs-lookup"><span data-stu-id="3cdd2-122">Your API's swagger appears.</span></span>

    ![Edit an api](./media/edit-api/edit-api003.png)

3. <span data-ttu-id="3cdd2-124">Update the swagger.</span><span class="sxs-lookup"><span data-stu-id="3cdd2-124">Update the swagger.</span></span>
4. <span data-ttu-id="3cdd2-125">Press **Save**.</span><span class="sxs-lookup"><span data-stu-id="3cdd2-125">Press **Save**.</span></span>

[!INCLUDE [api-management-define-api-topics.md](../../includes/api-management-define-api-topics.md)]

## <a name="next-steps"></a><span data-ttu-id="3cdd2-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="3cdd2-126">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="3cdd2-127">[APIM policy samples](policy-samples.md)
> [Transform and protect a published API](transform-api.md)</span><span class="sxs-lookup"><span data-stu-id="3cdd2-127">[APIM policy samples](policy-samples.md)
[Transform and protect a published API](transform-api.md)</span></span>