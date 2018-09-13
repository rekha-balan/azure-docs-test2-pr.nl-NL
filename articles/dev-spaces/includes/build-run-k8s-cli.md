---
title: include file
description: include file
ms.custom: include file
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: ghogen
ms.author: ghogen
ms.date: 05/11/2018
ms.topic: include
manager: douge
ms.openlocfilehash: b18cfce173da562aa7cffa48f336ff623c868f21
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45181302"
---
## <a name="build-and-run-code-in-kubernetes"></a>Build and run code in Kubernetes
Let's run our code! In the terminal window, run this command from the **root code folder**, webfrontend:

```cmd
azds up
```

Keep an eye on the command's output, you'll notice several things as it progresses:
- Source code is synced to the dev space in Azure.
- A container image is built in Azure, as specified by the Docker assets in your code folder.
- Kubernetes objects are created that utilize the container image as specified by the Helm chart in your code folder.
- Information about the container's endpoint(s) is displayed. In our case, we're expecting a public HTTP URL.
- Assuming the above stages complete successfully, you should begin to see `stdout` (and `stderr`) output as the container starts up.

> [!Note]
> These steps will take longer the first time the `up` command is run, but subsequent runs should be quicker.

### <a name="test-the-web-app"></a>Test the web app
Scan the console output for information about the public URL that was created by the `up` command. It will be in the form: 

`Service 'webfrontend' port 'http' is available at <url>` 

Open this URL in a browser window, and you should see the web app load. As the container executes, `stdout` and `stderr` output is streamed to the terminal window.

> [!Note]
> On first run, it can take several minutes for public DNS to be ready. If the public URL does not resolve, you can use the alternative http://localhost:<portnumber> URL that is displayed in the console output. If you use the localhost URL, it may seem like the container is running locally, but actually it is running in AKS. For your convenience, and to facilitate interacting with the service from your local machine, Azure Dev Spaces creates a temporary SSH tunnel to the container running in Azure. You can come back and try the public URL later when the DNS record is ready.
