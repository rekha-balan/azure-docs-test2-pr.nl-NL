---
title: Avoid service interruptions in Azure Stream Analytics jobs
description: This article describes guidance on making your Stream Analytics jobs upgrade resilient.
services: stream-analytics
author: jseb225
manager: kfile
ms.author: jeanb
ms.reviewer: jasonh
ms.service: stream-analytics
ms.topic: conceptual
ms.date: 03/28/2017
ms.openlocfilehash: 47ccfe99d2ee6576dbb70324eb383f52d2a1b2e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44797581"
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>Guarantee Stream Analytics job reliability during service updates

Part of being a fully managed service is the capability to introduce new service functionality and improvements at a rapid pace. As a result, Stream Analytics can have a service update deploy on a weekly (or more frequent) basis. No matter how much testing is done there is still a risk that an existing, running job may break due to the introduction of a bug. For customers who run critical streaming processing jobs these risks need to be avoided. A mechanism customers can use to reduce this risk is Azure’s **[paired region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** model. 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>How do Azure paired regions address this concern?

Stream Analytics guarantees jobs in paired regions are updated in separate batches. As a result there is a sufficient time gap between the updates to identify potential breaking bugs and remediate them.

_With the exception of Central India_ (whose paired region, South India, does not have Stream Analytics presence), the deployment of an update to Stream Analytics would not occur at the same time in a set of paired regions. Deployments in multiple regions **in the same group** may occur **at the same time**.

The article on **[availability and paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** has the most up-to-date information on which regions are paired.

Customers are advised to deploy identical jobs to both paired regions. In addition to Stream Analytics internal monitoring capabilities, customers are also advised to monitor the jobs as if **both** are production jobs. If a break is identified to be a result of the Stream Analytics service update, escalate appropriately and fail over any downstream consumers to the healthy job output. Escalation to support will prevent the paired region from being affected by the new deployment and maintain the integrity of the paired jobs.
