---
title: Install the DC/OS CLI | Microsoft Docs
description: Install the DC/OS CLI.
services: container-service
documentationcenter: ''
author: rgardler
manager: timlt
editor: ''
tags: acs, azure-container-service
keywords: Containers, Micro-services, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2016
ms.author: rogardle
ms.openlocfilehash: a8ea47f158c0d666340815d2e039995c7483257f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556231"
---
> [!NOTE]
> <span data-ttu-id="dcb8b-104">This is for working with DC/OS-based ACS clusters.</span><span class="sxs-lookup"><span data-stu-id="dcb8b-104">This is for working with DC/OS-based ACS clusters.</span></span> <span data-ttu-id="dcb8b-105">There is no need to do this for Swarm-based ACS clusters.</span><span class="sxs-lookup"><span data-stu-id="dcb8b-105">There is no need to do this for Swarm-based ACS clusters.</span></span>
> 
> 

<span data-ttu-id="dcb8b-106">First, [connect to your DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="dcb8b-106">First, [connect to your DC/OS-based ACS cluster](../articles/container-service/container-service-connect.md).</span></span> <span data-ttu-id="dcb8b-107">Once you have done this, you can install the DC/OS CLI on your client machine with the commands below:</span><span class="sxs-lookup"><span data-stu-id="dcb8b-107">Once you have done this, you can install the DC/OS CLI on your client machine with the commands below:</span></span>

```bash
sudo pip install virtualenv
mkdir dcos && cd dcos
wget https://raw.githubusercontent.com/mesosphere/dcos-cli/master/bin/install/install-optout-dcos-cli.sh
chmod +x install-optout-dcos-cli.sh
./install-optout-dcos-cli.sh . http://localhost --add-path yes
```

<span data-ttu-id="dcb8b-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span><span class="sxs-lookup"><span data-stu-id="dcb8b-108">If you are using an old version of Python, you may notice some "InsecurePlatformWarnings".</span></span> <span data-ttu-id="dcb8b-109">You can safely ignore these.</span><span class="sxs-lookup"><span data-stu-id="dcb8b-109">You can safely ignore these.</span></span>

<span data-ttu-id="dcb8b-110">In order to get started without restarting your shell, run:</span><span class="sxs-lookup"><span data-stu-id="dcb8b-110">In order to get started without restarting your shell, run:</span></span>

```bash
source ~/.bashrc
```

<span data-ttu-id="dcb8b-111">This step will not be necessary when you start new shells.</span><span class="sxs-lookup"><span data-stu-id="dcb8b-111">This step will not be necessary when you start new shells.</span></span>

<span data-ttu-id="dcb8b-112">Now you can confirm that the CLI is installed:</span><span class="sxs-lookup"><span data-stu-id="dcb8b-112">Now you can confirm that the CLI is installed:</span></span>

```bash
dcos --help
```