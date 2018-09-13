---
title: List all of your Azure Import/Export jobs| MicrosoftDocs
description: Learn how to list all of the Azure Import/Export service jobs in a subscription.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: f2e619be-1bbd-4a54-9472-9e2f70a83b64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 1977bfc0e516088310f45ecdd960287eeed2c2d8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552856"
---
# <a name="enumerating-jobs-in-the-azure-importexport-service"></a><span data-ttu-id="92a0d-103">Enumerating jobs in the Azure Import/Export service</span><span class="sxs-lookup"><span data-stu-id="92a0d-103">Enumerating jobs in the Azure Import/Export service</span></span>
<span data-ttu-id="92a0d-104">To enumerate all jobs in a subscription, call the [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List) operation.</span><span class="sxs-lookup"><span data-stu-id="92a0d-104">To enumerate all jobs in a subscription, call the [List Jobs](/rest/api/storageimportexport/jobs#Jobs_List) operation.</span></span> <span data-ttu-id="92a0d-105">`List Jobs` returns a list of jobs as well as the following attributes:</span><span class="sxs-lookup"><span data-stu-id="92a0d-105">`List Jobs` returns a list of jobs as well as the following attributes:</span></span>

-   <span data-ttu-id="92a0d-106">The type of job (Import or Export)</span><span class="sxs-lookup"><span data-stu-id="92a0d-106">The type of job (Import or Export)</span></span>

-   <span data-ttu-id="92a0d-107">The current job state</span><span class="sxs-lookup"><span data-stu-id="92a0d-107">The current job state</span></span>

-   <span data-ttu-id="92a0d-108">The job's associated storage account</span><span class="sxs-lookup"><span data-stu-id="92a0d-108">The job's associated storage account</span></span>

## <a name="next-steps"></a><span data-ttu-id="92a0d-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="92a0d-109">Next steps</span></span>

* [<span data-ttu-id="92a0d-110">Using the Import/Export service REST API</span><span class="sxs-lookup"><span data-stu-id="92a0d-110">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
