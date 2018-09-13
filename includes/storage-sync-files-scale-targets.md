---
title: include file
description: include file
services: storage
author: wmgries
ms.service: storage
ms.topic: include
ms.date: 07/18/2018
ms.author: wgries
ms.custom: include file
ms.openlocfilehash: 5333655fe9d790e7768de35a6632124c99fa7e1e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45015928"
---
| Resource | Target | Hard limit |
|----------|--------------|------------|
| Storage Sync Services per subscription | 15 Storage Sync Services | No |
| Sync groups per Storage Sync Service | 100 sync groups | Yes |
| Registered servers per Storage Sync Service | 99 servers | Yes |
| Cloud endpoints per Sync Group | 1 cloud endpoint | Yes |
| Server endpoints per Sync Group | 50 server endpoints | No |
| Server endpoints per server | 33-99 server endpoints | Yes, but varies based on configuration (CPU, memory, volumes, file churn, file count, etc.) |
| Endpoint size | 4 TiB | No |
| File system objects (directories and files) per sync group | 25 million objects | No |
| Maximum number of file system objects (directories and files) in a directory | 200,000 objects | Yes |
| Maximum object (directories and files) name length | 255 characters | Yes |
| Maximum object (directories and files) security descriptor size | 4 KiB | Yes |
| File size | 100 GiB | No |
| Minimum file size for a file to be tiered | 64 KiB | Yes |
