---
title: Sign ins from multiple geographies
description: A report that indicates users where two sign ins appeared to originate from different regions and the time between the sign ins makes it impossible for the user to have travelled between those regions.
services: active-directory
documentationcenter: ''
author: SSalahAhmed
manager: gchander
editor: ''
ms.assetid: 79259c8a-2388-4747-b41e-c07434ea9a02
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 99738bfeedf53a826f32f6ae0dcc8de06cb17214
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563123"
---
# <a name="sign-ins-from-multiple-geographies"></a>Sign-ins from multiple geographies
This report includes successful sign-ins from a user where two sign-ins appeared to originate from different regions and the time between the sign-ins makes it impossible for the user to have traveled between those regions. Possible causes include:

* User is sharing their password with other users
* User is using a remote desktop to launch a web browser for sign-in
* A hacker has signed in to the account of a user from a different country
* User is using a VPN or proxy
* User is signed in from multiple devices at the same time, such as a desktop and a mobile phone, and the IP address of the mobile phone is unusual.

Results from this report will show you the successful sign-in events, together with the time between the sign-ins, the regions where the sign-ins appeared to originate from, and the estimated travel time between those regions. The travel time shown is only an estimate and may be different from the actual travel time between the locations.

![Sign ins from multiple geographies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-sign-ins-from-multiple-geographies/signInsFromMultipleGeographies.PNG)


