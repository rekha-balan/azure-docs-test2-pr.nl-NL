---
title: Azure Batch render manager support
description: Using Azure for rendering using Azure Batch render manager integration
services: batch
author: mscurrell
ms.author: markscu
ms.date: 08/02/2018
ms.topic: conceptual
ms.openlocfilehash: 798b2b457016856662f392af25d987788f73c242
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866898"
---
# <a name="using-azure-batch-with-render-farm-managers"></a>Using Azure Batch with render farm managers

If you're using an existing on-premises render farm, then it's highly likely that a render manager controls the render farm capacity and render jobs.

Azure provides either built-in support or add-ons for popular render managers. You can then add and remove Azure VMs, including VMs with the pay-for-use application licensing and low-priority VMs.

The following render managers are supported:

* [PipelineFX Qube!](https://www.pipelinefx.com/)
* [Royal Render](http://www.royalrender.de/)
* [Thinkbox Deadline](https://deadline.thinkboxsoftware.com/)

## <a name="using-azure-with-pipelinefx-qube"></a>Using Azure with PipelineFX Qube

Scripts and instructions to enable Azure Batch pool VMs to be used as Qube workers are in [the GitHub repository](https://github.com/Azure/azure-qube).

## <a name="using-azure-with-royal-render"></a>Using Azure with Royal Render

Royal Render has Azure and Azure Batch integration built-in, allowing you to extend a render farm with Azure-based VMs. For a summary, see [the help files](http://www.royalrender.de/help8/index.html?Cloudrendering.html).

For an example of a Royal Render customer using the Azure integration, see the [Jellyfish Pictures customer story](https://customers.microsoft.com/en-gb/story/jellyfishpictures).

## <a name="using-azure-with-thinkbox-deadline"></a>Using Azure with Thinkbox Deadline

Scripts and instructions to enable Azure Batch pool VMs to be used as Deadline slaves are in [the GitHub repository](https://github.com/Azure/azure-deadline).

## <a name="next-steps"></a>Next steps

Try out the Azure Batch integration for your render manager, using the appropriate plug-in and instructions on GitHub, where applicable.