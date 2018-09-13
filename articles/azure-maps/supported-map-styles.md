---
title: Supported map styles in Azure Maps| Microsoft Docs
description: Map styles supported by Azure Maps
author: walsehgal
ms.author: v-musehg
ms.date: 08/28/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.openlocfilehash: 8f0910e9040c962bae30a33b91a93e71e692dfdb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966572"
---
# <a name="azure-maps-supported-map-styles"></a>Azure Maps supported map styles
Azure maps support four different built-in map styles. The styles along with their descriptions are listed below.

## <a name="road"></a>Road
A **road** map is a standard map that displays roads, natural and man-made features along with the labels for those features.

![road](./media/supported-map-styles/road.png)

**Applicable APIs:**
* [Map image](https://docs.microsoft.com/rest/api/maps/render/getmapimage)
* [Map tile](https://docs.microsoft.com/rest/api/maps/render/getmaptile)
* JS map control

## <a name="satellite"></a>Satellite 
The **satellite** style is a combination of satellite and aerial imagery.

![satellite](./media/supported-map-styles/satellite.png)

**Applicable APIs:**
* [Satellite tile](https://docs.microsoft.com/rest/api/maps/render/getmapimagerytilepreview)
* JS map control

## <a name="satelliteroadlabels"></a>Satellite_Road_Labels
This map style is a hybrid of roads and labels overlaid on top of satellite and aerial imagery.

![satellite_road_labels](./media/supported-map-styles/satellite_road_labels.png)

**Applicable APIs:**
* JS map control

## <a name="grayscaledark"></a>Grayscale_Dark
**Grayscale dark** is a dark version of the road map style.

![gray_scale](./media/supported-map-styles/grayscale_dark.png)

**Applicable APIs:**
* JS map control 