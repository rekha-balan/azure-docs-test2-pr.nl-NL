---
title: Batch Analytics - Azure | Microsoft Docs
ms.custom: ''
ms.date: 2017-02-01
ms.prod: azure
ms.reviewer: ''
ms.service: batch
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2fda4d9c-f782-4088-9320-656b450e3100
caps.latest.revision: 7
author: tamram
ms.author: tamram
manager: timlt
ms.openlocfilehash: 4b73637e0ec6798b701d5a13f96c504bcbb14cc7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552574"
---
# <a name="batch-analytics"></a>Batch Analytics
The topics in Batch Analytics contain reference information for the events and alerts available for Batch service resources.

See [Azure Batch diagnostic logging](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) for more information on enabling and consuming Batch diagnostic logs.

## <a name="diagnostic-logs"></a>Diagnostic logs

The Azure Batch service emits the following diagnostic log events during the lifetime of certain Batch resources.

**Service Log events**
* [Pool create](batch-pool-create-event.md)
* [Pool delete start](batch-pool-delete-start-event.md)
* [Pool delete complete](batch-pool-delete-complete-event.md)
* [Pool resize start](batch-pool-resize-start-event.md)
* [Pool resize complete](batch-pool-resize-complete-event.md)
* [Task start](batch-task-start-event.md)
* [Task complete](batch-task-complete-event.md)
* [Task fail](batch-task-fail-event.md)