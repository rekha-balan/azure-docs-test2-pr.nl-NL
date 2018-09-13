---
title: Sign ins from possibly infected devices
description: A report that includes sign in attempts that have been executed from devices on which some malware (malicious software) may be running.
services: active-directory
documentationcenter: ''
author: SSalahAhmed
manager: gchander
editor: ''
ms.assetid: d0361662-d970-4a66-8eb3-72e9f8824dcf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: debbfa8647c979a2d10bf5e773386e10018c205a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553730"
---
# <a name="sign-ins-from-possibly-infected-devices"></a>Sign ins from possibly infected devices
This report attempts to identify your users' devices that that have become infected and are now part of a botnet. We correlate IP addresses of users' sign-ins against IP addresses that we know to be in contact with botnet servers.

Recommendation: This report flags IP addresses, not user devices. We recommend that you contact the user and scan all the user's devices to be certain. It is also possible that a user's personal device is infected, or that someone other than the user, who was using the same IP address as the user, has an infected device.

For more information about how to address malware infections, see the [Malware Protection Center](http://go.microsoft.com/fwlink/?linkid=335773).

![Sign ins from possibly infected devices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-sign-ins-from-possibly-infected-devices/signInsFromPossiblyInfectedDevices.PNG)


