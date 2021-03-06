---
title: include file
description: include file
services: functions
author: ggailey777
manager: cfowler
ms.service: functions
ms.topic: include
ms.date: 05/01/2018
ms.author: glenga
ms.custom: include file
ms.openlocfilehash: 88c01e8e57d4a92478b8b1ca0689ff0f8e499b39
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45376421"
---
When the Functions host runs locally, it writes logs to the following path:

```
<DefaultTempDirectory>\LogFiles\Application\Functions
```

On Windows, `<DefaultTempDirectory>` is the first found value of the TMP, TEMP, USERPROFILE environment variables, or the Windows directory.
On MacOS or Linux, `<DefaultTempDirectory>` is the TMPDIR environment variable.

> [!NOTE]
> When the Functions host starts, it overwrites the existing file structure in the directory.