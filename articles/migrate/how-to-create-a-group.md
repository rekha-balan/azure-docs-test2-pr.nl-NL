---
title: Group machines for assessment with Azure Migrate | Microsoft Docs
description: Describes how to group machines before you run an assessment with the Azure Migrate service.
author: rayne-wiselman
ms.service: azure-migrate
ms.topic: article
ms.date: 06/19/2018
ms.author: raynew
ms.openlocfilehash: ccab88c0195a7ca459c8579b7870d121dfd0fe1d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966714"
---
# <a name="group-machines-for-assessment"></a>Group machines for assessment

This article describes how to create a group of machines for assessment by [Azure Migrate](migrate-overview.md). Azure Migrate assesses machines in the group to check whether they're suitable for migration to Azure, and provides sizing and cost estimations for running the machine in Azure.


## <a name="create-a-group"></a>Create a group

1. In the **Overview** of the Azure Migrate project, under Manage, click **Groups** > **+Group**, and specify a group name.
2. Add one or more machines to the group, and click **Create**. 
3. You can optionally select to run a new assessment for the group. 

    ![Create a group](./media/how-to-create-a-group/create-group.png)

After the group is created, you can modify it by selecting the group on the **Groups** page, and adding or removing machines.

## <a name="next-steps"></a>Next steps

- Learn how to use [machine dependency mapping](how-to-create-group-machine-dependencies.md) to create high confidence groups.
- [Learn more](concepts-assessment-calculation.md) about how assessments are calculated.
