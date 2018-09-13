---
title: Overview of Custom Vision Service machine learning - Azure Cognitive Services | Microsoft Docs
description: The Custom Vision Service is a Microsoft Cognitive Service that lets you build custom image classifiers on the Azure platform.
services: cognitive-services
author: anrothMSFT
manager: corncar
ms.service: cognitive-services
ms.component: custom-vision
ms.topic: overview
ms.date: 05/02/2018
ms.author: anroth
ms.openlocfilehash: d2daf7c211f9474f5636b6af69c5b700d597aa14
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968903"
---
# <a name="what-is-the-custom-vision-service"></a>What is the Custom Vision Service?

The Custom Vision Service is a Microsoft Cognitive Service that lets you build custom image classifiers. It makes it easy and fast to build, deploy, and improve an image classifier. The Custom Vision Service provides a REST API and a web interface to upload your images and train the classifier.

## <a name="what-does-custom-vision-service-do-well"></a>What does Custom Vision Service do well?

The Custom Vision Service works best when the item you're trying to classify is prominent in your image. 

Few images are required to create a classifier or detector. 50 images per class are enough to start your prototype. The methods Custom Vision Service uses are robust to differences, which allows you to start prototyping with so little data. This means Custom Vision Service is not well suited to scenarios where you want to detect subtle differences. For example, minor cracks or dents in quality assurance scenarios.

## <a name="next-steps"></a>Next steps

[Learn how to build a classifier](getting-started-build-a-classifier.md)
