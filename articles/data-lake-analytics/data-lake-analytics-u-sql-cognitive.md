---
title: Using U-SQL Cognitive capabilities in Azure Data Lake Analytics | Microsoft Docs
description: Learn how to use the intelligence of Cognitive capabilities in U-SQL
services: data-lake-analytics
documentationcenter: ''
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: 019c1d53-4e61-4cad-9b2c-7a60307cbe19
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: 596459e25f8ad072a55ad45a2f444c71b27fd60c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562819"
---
# <a name="tutorial-get-started-with-the-cognitive-capabilities-of-u-sql"></a><span data-ttu-id="040fd-103">Tutorial: Get started with the Cognitive capabilities of U-SQL</span><span class="sxs-lookup"><span data-stu-id="040fd-103">Tutorial: Get started with the Cognitive capabilities of U-SQL</span></span>

<span data-ttu-id="040fd-104">Cognitive capabilities for U-SQL enable developers to use put intelligence in their big data programs.</span><span class="sxs-lookup"><span data-stu-id="040fd-104">Cognitive capabilities for U-SQL enable developers to use put intelligence in their big data programs.</span></span> <span data-ttu-id="040fd-105">The overall process in simple:</span><span class="sxs-lookup"><span data-stu-id="040fd-105">The overall process in simple:</span></span>

* <span data-ttu-id="040fd-106">Use the REFERENCE ASSEMBLY statement to enable the cognitive features for the U-SQL Script</span><span class="sxs-lookup"><span data-stu-id="040fd-106">Use the REFERENCE ASSEMBLY statement to enable the cognitive features for the U-SQL Script</span></span>
* <span data-ttu-id="040fd-107">Using the PROCESS operation to use the Cognitive capabilities</span><span class="sxs-lookup"><span data-stu-id="040fd-107">Using the PROCESS operation to use the Cognitive capabilities</span></span> 

## <a name="imaging-scenarios"></a><span data-ttu-id="040fd-108">Imaging Scenarios</span><span class="sxs-lookup"><span data-stu-id="040fd-108">Imaging Scenarios</span></span>

### <a name="a-simple-example-image-tagging"></a><span data-ttu-id="040fd-109">A Simple Example: Image Tagging</span><span class="sxs-lookup"><span data-stu-id="040fd-109">A Simple Example: Image Tagging</span></span>

<span data-ttu-id="040fd-110">The following example shows and end-to-end use of the imaging capabilities to detect objects in images.</span><span class="sxs-lookup"><span data-stu-id="040fd-110">The following example shows and end-to-end use of the imaging capabilities to detect objects in images.</span></span>

    REFERENCE ASSEMBLY ImageCommon;
    REFERENCE ASSEMBLY FaceSdk;
    REFERENCE ASSEMBLY ImageEmotion;
    REFERENCE ASSEMBLY ImageTagging;
    REFERENCE ASSEMBLY ImageOcr;

    @imgs =
        EXTRACT FileName string, ImgData byte[]
        FROM @"/images/{FileName:*}.jpg"
        USING new Cognition.Vision.ImageExtractor();

    // Extract the number of objects on each image and tag them 
    @objects =
        PROCESS @imgs 
        PRODUCE FileName,
                NumObjects int,
                Tags string
        READONLY FileName
        USING new Cognition.Vision.ImageTagger();


### <a name="extract-emotions-from-human-faces"></a><span data-ttu-id="040fd-111">Extract emotions from human faces</span><span class="sxs-lookup"><span data-stu-id="040fd-111">Extract emotions from human faces</span></span> 

    @emotions =
        PROCESS @imgs
        PRODUCE FileName string,
                NumFaces int,
                Emotion string
        READONLY FileName
        USING new Cognition.Vision.EmotionAnalyzer();

### <a name="estimate-age-and-gender-for-human-faces"></a><span data-ttu-id="040fd-112">Estimate age and gender for human faces</span><span class="sxs-lookup"><span data-stu-id="040fd-112">Estimate age and gender for human faces</span></span>

    @faces = 
            PROCESS @imgs
            PRODUCE FileName,
                    NumFaces int,
                    FaceAge string,
                    FaceGender string
            READONLY FileName
            USING new Cognition.Vision.FaceDetector();

### <a name="detect-text-in-images-ocr"></a><span data-ttu-id="040fd-113">Detect text in Images (OCR)</span><span class="sxs-lookup"><span data-stu-id="040fd-113">Detect text in Images (OCR)</span></span>

    @ocrs =
            PROCESS @imgs
            PRODUCE FileName,
                    Text string
            READONLY FileName
            USING new Cognition.Vision.OcrExtractor();

## <a name="text-scenarios"></a><span data-ttu-id="040fd-114">Text Scenarios</span><span class="sxs-lookup"><span data-stu-id="040fd-114">Text Scenarios</span></span>

### <a name="input-data"></a><span data-ttu-id="040fd-115">Input data</span><span class="sxs-lookup"><span data-stu-id="040fd-115">Input data</span></span>

<span data-ttu-id="040fd-116">Assume that we have an input that consists of “War and Peace” by Leo Tolstoy.</span><span class="sxs-lookup"><span data-stu-id="040fd-116">Assume that we have an input that consists of “War and Peace” by Leo Tolstoy.</span></span>

    REFERENCE ASSEMBLY [TextCommon];
    REFERENCE ASSEMBLY [TextSentiment];
    REFERENCE ASSEMBLY [TextKeyPhrase];

    @WarAndPeace =
        EXTRACT No int,
                Year string,
                Book string,
                Chapter string,
                Text string
        FROM @"/usqlext/samples/cognition/war_and_peace.csv"
        USING Extractors.Csv();

### <a name="extract-key-phrases-for-each-paragraph"></a><span data-ttu-id="040fd-117">Extract key phrases for each paragraph.</span><span class="sxs-lookup"><span data-stu-id="040fd-117">Extract key phrases for each paragraph.</span></span>

    @keyphrase =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                KeyPhrase string
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.KeyPhraseExtractor();

    // Tokenize the key phrases.
    @kpsplits =
        SELECT No,
            Year,
            Book,
            Chapter,
            Text,
            T.KeyPhrase
        FROM @keyphrase
            CROSS APPLY
                new Cognition.Text.Splitter("KeyPhrase") AS T(KeyPhrase);
    
### <a name="perform-sentiment-analysis-on-each-paragraph"></a><span data-ttu-id="040fd-118">Perform sentiment analysis on each paragraph</span><span class="sxs-lookup"><span data-stu-id="040fd-118">Perform sentiment analysis on each paragraph</span></span>

    @sentiment =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                Sentiment string,
                Conf double
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.SentimentAnalyzer(true);

