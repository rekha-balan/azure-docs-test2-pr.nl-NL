---
title: Copy others' data science examples – machine learning - Azure | Microsoft Docs
description: 'Trade secret of data science: Get others to do your work for you. Get machine learning examples from the Cortana Analytics Gallery.'
keywords: data science examples,machine learning example,clustering algorithm,clustering algorithm example
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: ec2be823-c325-4ad8-b8b2-3e664f1a44b4
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/09/2017
ms.author: cgronlun;garye
ms.openlocfilehash: ae31a8f478101a7fef1c6073cfb6d37fcab31058
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564732"
---
# <a name="copy-other-peoples-work-to-do-data-science"></a>Copy other people's work to do data science
## <a name="video-5-data-science-for-beginners-series"></a>Video 5: Data Science for Beginners series
One of the trade secrets of data science is getting other people to do your work for you. Find a clustering algorithm example in Cortana Analytics Gallery to use for your own machine learning experiment.

To get the most out of the series, watch them all. [Go to the list of videos](#other-videos-in-this-series)

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/data-science-for-beginners-series-copy-other-peoples-work-to-do-data-science/player]
>
>

## <a name="other-videos-in-this-series"></a>Other videos in this series
*Data Science for Beginners* is a quick introduction to data science in five short videos.

* Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*
* Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md) *(4 min 56 sec)*
* Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*
* Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*
* Video 5: Copy other people's work to do data science

## <a name="transcript-copy-other-peoples-work-to-do-data-science"></a>Transcript: Copy other people's work to do data science
Welcome to the fifth video in the series “Data Science for Beginners.”

In this one, you’ll discover a place to find examples that you can borrow from as a starting point for your own work. You might get the most out of this video if you first watch the earlier videos in this series.

One of the trade secrets of data science is getting other people to do your work for you.

## <a name="find-examples-in-the-cortana-intelligence-gallery"></a>Find examples in the Cortana Intelligence Gallery
Microsoft has a cloud-based service called [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) that you're welcome to try for free. It provides you with a workspace where you can experiment with different machine learning algorithms, and, when you've got your solution worked out, you can launch it as a web service.

Part of this service is something called the **[Cortana Intelligence Gallery](http://aka.ms/CortanaIntelligenceGallery)**. It contains a variety of resources, one of which is a collection of Azure Machine Learning experiments, or models, that people have built and contributed for others to use. These experiments are a great way to leverage the thought and hard work of others to get you started on your own solutions.

You can find the gallery at [aka.ms/CortanaIntelligenceGallery](http://aka.ms/CortanaIntelligenceGallery). Everyone is welcome to browse through it.

![Cortana Intelligence Gallery](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/cortana-intelligence-gallery.png)

If you click **Experiments** at the top, you'll see a number of the most recent and popular experiments in the gallery. You can search through the rest of experiments by clicking **Browse All** at the top of the screen, and there you can enter search terms and choose search filters.

## <a name="find-and-use-a-clustering-algorithm-example"></a>Find and use a clustering algorithm example
So, for instance, let's say you want to see an example of how clustering works, so you search for **"clustering"** experiments.

![Search for clustering experiments](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/search-for-clustering-experiments.png)

Here's an interesting one that someone contributed to the gallery.

![Clustering experiment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/clustering-experiment.png)

Click on that experiment and you get a web page that describes the work that this contributor did, along with some of their results.

![Clustering experiment description page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/clustering-experiment-description-page.png)

Notice the link that says **Open in Studio**.

![Open in Studio button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/open-in-studio.png)

I can click on that and it takes me right to **Azure Machine Learning Studio**. It creates a copy of the experiment and puts it in my own workspace. This includes the contributor's dataset, all the processing that they did, all of the algorithms that they used, and how they saved out the results.

![Open a Gallery experiment in Machine Learning Studio - clustering algorithm example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/cluster-experiment-open-in-studio.png)

And now I have a starting point. I can swap out their data for my own and do my own tweaking of the model. This gives me a running start, and it lets me build on the work of people who really know what they’re doing.

## <a name="find-experiments-that-demonstrate-machine-learning-techniques"></a>Find experiments that demonstrate machine learning techniques
There are other experiments in the [Cortana Intelligence Gallery](http://aka.ms/CortanaIntelligenceGallery) that were contributed specifically to provide how-to examples for people new to data science. For instance, there's an experiment in the gallery that demonstrates how to handle missing values ([Methods for handling missing values](https://gallery.cortanaintelligence.com/Experiment/Methods-for-handling-missing-values-1)). It walks you through 15 different ways of substituting empty values, and talks about the benefits of each method and when to use it.

![Gallery experiments open in Machine Learning Studio - methods for missing values](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science/experiment-methods-for-handling-missing-values.png)

[Cortana Intelligence Gallery](http://aka.ms/CortanaIntelligenceGallery) is a place to find working experiments that you can use as a starting point for your own solutions.

Be sure to check out the other videos in “Data Science for Beginners” from Microsoft Azure Machine Learning.

## <a name="next-steps"></a>Next steps
* [Try your first data science experiment with Azure Machine Learning](machine-learning-create-experiment.md)
* [Get an introduction to Machine Learning on Microsoft Azure](machine-learning-what-is-machine-learning.md)







