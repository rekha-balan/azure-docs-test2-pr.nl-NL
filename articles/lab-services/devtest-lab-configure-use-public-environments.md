---
title: Configure and use public environments in Azure DevTest Labs | Microsoft Docs
description: Learn how to configure and use public environments in Azure DevTest Labs.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/13/2018
ms.author: spelluru
ms.openlocfilehash: d93818cd875c4050b1b35f21ce580933776c5bc5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866341"
---
# <a name="configure-and-use-public-environments-in-azure-devtest-labs"></a>Configure and use public environments in Azure DevTest Labs
Azure DevTest Labs has a [public repository of Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/Environments) that you can use to create environments without having to connect to an external GitHub source by yourself. This repository includes frequently used templates such as Azure Web Apps, Service Fabric Cluster, and development SharePoint Farm environment. This feature is similar to the public repository of artifacts that is included for every lab that you create. The environment repository allows you to quickly get started with pre-authored environment templates with minimum input parameters to provide you with a smooth getting started experience for PaaS resources within labs. 

## <a name="configuring-public-environments"></a>Configuring public environments
As a lab owner, you can enable the public environment repository for your lab during the lab creation. To enable public environments for your lab, select **On** for the **Public environments** field while creating a lab. 

![Enable public environment for a new lab](media/devtest-lab-configure-use-public-environments/enable-public-environment-new-lab.png)


For existing labs, the public environment repository is not enabled. Manually enable it to use templates in the repository. For labs created using Resource Manager templates, the repository is disabled by default as well.

You can enable/disable public environments for your lab, and also make only specific environments available to lab users by using the following steps: 

1. Select **Configuration and policies** for your lab. 
2. In the **VIRTUAL MACHINE BASES** section, select **Public environments**.
3. To enable public environments for the lab, select **Yes**. Otherwise, select **No**. 
4. If you enabled public environments, all the environments in the repository are enabled by defaults. You can de-select an environment to make it not available to your lab users. 

![Public environments page](media/devtest-lab-configure-use-public-environments/public-environments-page.png)

## <a name="use-environment-templates-as-a-lab-user"></a>Use environment templates as a lab user
As a lab user, you can create a new environment from the enabled list of environment templates by simply selecting **+Add** from the tool bar in the lab page. The list of bases includes the public environments templates enabled by your lab admin at the top of the list.

![Public environment templates](media/devtest-lab-configure-use-public-environments/public-environment-templates.png)

## <a name="next-steps"></a>Next steps
This repository is an open-source repository that you can contribute to add frequently used and helpful Resource Manager templates of your own. To contribute, simply submit a pull request against the repository.  
