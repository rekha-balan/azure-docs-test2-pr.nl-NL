---
title: Enable Session Affinity using the Azure Toolkit for Eclipse
description: Learn how to enable session affinity using the Azure Toolkit for Eclipse.
services: ''
documentationcenter: java
author: rmcmurray
manager: erikre
editor: ''
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 11/01/2016
ms.author: robmcm
ms.openlocfilehash: 5a821a0f4ce55d4d6156e934e75b3fdb5b131024
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662463"
---
# <a name="enable-session-affinity"></a>Enable Session Affinity
Within the Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles. The following image shows the **Load Balancing** properties dialog used to enable the session affinity feature:

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a>To enable session affinity for your role
1. Right-click the role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.
2. In the **Properties for WorkerRole1 Load Balancing** dialog:
   1. Check **Enable HTTP session affinity (sticky sessions) for this role.**
   2. For **Input endpoint to use**, select an input endpoint to use, for example, **http (public:80, private:8080)**. Your application must use this endpoint as its HTTP endpoint. You can enable multiple endpoints for your role, but you can select only one of them to support sticky sessions.
   3. Rebuild your application.

Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by the same role instance.

The Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances. ARR reroutes HTTP requests to the appropriate role instance. The toolkit automatically reconfigures the selected endpoint so that the incoming HTTP traffic is first routed to the ARR software. The toolkit also creates a new internal endpoint that your Java server is configured to listen to. That is the endpoint used by ARR to reroute the HTTP traffic to the appropriate role instance. This way, each role instance in your multi-instance deployment serves as a reverse proxy for all the other instances, enabling sticky sessions.

## <a name="notes-about-session-affinity"></a>Notes about session affinity
* Session affinity does not work in the compute emulator. The settings can be applied in the compute emulator without interfering with your build process or compute emulator execution, but the feature itself does not function within the compute emulator.
* Enabling session affinity will result in an increase in the amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in the Azure cloud.
* The time to initialize each role will take longer.
* An internal endpoint, to function as a traffic rerouter as mentioned above, will be added.


## <a name="see-also"></a>See Also
[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]

[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse] 

For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->

