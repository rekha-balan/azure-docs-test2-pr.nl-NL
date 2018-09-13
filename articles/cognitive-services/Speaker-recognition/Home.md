---
title: Speaker Recognition API | Microsoft Docs
description: Use advanced algorithms for speaker verification and speaker identification with the Speaker Recognition API in Cognitive Services.
services: cognitive-services
author: dwlin
manager: zhang
ms.service: cognitive-services
ms.technology: speaker-recognition
ms.topic: article
ms.date: 03/20/2016
ms.author: dwlin
ms.openlocfilehash: 4f8ba17ae7e0de1f97ae1355c41d33699a5bbb86
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548725"
---
# <a name="speaker-recognition-api"></a><span data-ttu-id="a44bd-103">Speaker Recognition API</span><span class="sxs-lookup"><span data-stu-id="a44bd-103">Speaker Recognition API</span></span>

<span data-ttu-id="a44bd-104">Welcome to the Microsoft Speaker Recognition APIs.</span><span class="sxs-lookup"><span data-stu-id="a44bd-104">Welcome to the Microsoft Speaker Recognition APIs.</span></span> <span data-ttu-id="a44bd-105">Speaker Recognition APIs are cloud-based APIs that provide the most advanced algorithms for speaker verification and speaker identification.</span><span class="sxs-lookup"><span data-stu-id="a44bd-105">Speaker Recognition APIs are cloud-based APIs that provide the most advanced algorithms for speaker verification and speaker identification.</span></span> <span data-ttu-id="a44bd-106">Speaker Recognition can be divided into two categories: speaker verification and speaker identification.</span><span class="sxs-lookup"><span data-stu-id="a44bd-106">Speaker Recognition can be divided into two categories: speaker verification and speaker identification.</span></span>


## <a name="speaker-verification"></a><span data-ttu-id="a44bd-107">Speaker Verification</span><span class="sxs-lookup"><span data-stu-id="a44bd-107">Speaker Verification</span></span>


<span data-ttu-id="a44bd-108">Voice has unique characteristics that can be used to identify a person, just like a fingerprint.</span><span class="sxs-lookup"><span data-stu-id="a44bd-108">Voice has unique characteristics that can be used to identify a person, just like a fingerprint.</span></span>  <span data-ttu-id="a44bd-109">Using voice as a signal for access control and authentication scenarios has emerged as a new innovative tool –essentially offering a level up in security that simplifies the authentication experience for customers.</span><span class="sxs-lookup"><span data-stu-id="a44bd-109">Using voice as a signal for access control and authentication scenarios has emerged as a new innovative tool –essentially offering a level up in security that simplifies the authentication experience for customers.</span></span>

<span data-ttu-id="a44bd-110">Speaker Verification APIs can automatically verify and authenticate users using their voice or speech.</span><span class="sxs-lookup"><span data-stu-id="a44bd-110">Speaker Verification APIs can automatically verify and authenticate users using their voice or speech.</span></span>

### <a name="enrollment"></a><span data-ttu-id="a44bd-111">Enrollment</span><span class="sxs-lookup"><span data-stu-id="a44bd-111">Enrollment</span></span>

<span data-ttu-id="a44bd-112">Enrollment for speaker verification is text-dependent, which means speakers need to choose a specific pass phrase to use during both enrollment and verification phases.</span><span class="sxs-lookup"><span data-stu-id="a44bd-112">Enrollment for speaker verification is text-dependent, which means speakers need to choose a specific pass phrase to use during both enrollment and verification phases.</span></span> 

<span data-ttu-id="a44bd-113">In enrollment, the speaker's voice is recorded saying a specific phrase, then a number of features are extracted and the chosen phrase is recognized.</span><span class="sxs-lookup"><span data-stu-id="a44bd-113">In enrollment, the speaker's voice is recorded saying a specific phrase, then a number of features are extracted and the chosen phrase is recognized.</span></span> <span data-ttu-id="a44bd-114">Together, both extracted features and the chosen phrase form a unique voice signature.</span><span class="sxs-lookup"><span data-stu-id="a44bd-114">Together, both extracted features and the chosen phrase form a unique voice signature.</span></span>

### <a name="verification"></a><span data-ttu-id="a44bd-115">Verification</span><span class="sxs-lookup"><span data-stu-id="a44bd-115">Verification</span></span>
###
<span data-ttu-id="a44bd-116">In verification, an input voice and phrase are compared against the enrollment's voice signature and phrase –in order to verify whether or not they are from the same person, and if they are saying the correct phrase.</span><span class="sxs-lookup"><span data-stu-id="a44bd-116">In verification, an input voice and phrase are compared against the enrollment's voice signature and phrase –in order to verify whether or not they are from the same person, and if they are saying the correct phrase.</span></span>

<span data-ttu-id="a44bd-117">For more details about speaker verification, please refer to the API [Speaker - Verification](https://westus.dev.cognitive.microsoft.com/docs/services/563309b6778daf02acc0a508/operations/563309b7778daf06340c9652).</span><span class="sxs-lookup"><span data-stu-id="a44bd-117">For more details about speaker verification, please refer to the API [Speaker - Verification](https://westus.dev.cognitive.microsoft.com/docs/services/563309b6778daf02acc0a508/operations/563309b7778daf06340c9652).</span></span>

## <a name="speaker-identification"></a><span data-ttu-id="a44bd-118">Speaker Identification</span><span class="sxs-lookup"><span data-stu-id="a44bd-118">Speaker Identification</span></span>

<span data-ttu-id="a44bd-119">Speaker Identification APIs can automatically identify the person speaking in an audio file, given a group of prospective speakers.</span><span class="sxs-lookup"><span data-stu-id="a44bd-119">Speaker Identification APIs can automatically identify the person speaking in an audio file, given a group of prospective speakers.</span></span> <span data-ttu-id="a44bd-120">The input audio is paired against the provided group of speakers, and in the case that there is a match found, the speaker’s identity is returned.</span><span class="sxs-lookup"><span data-stu-id="a44bd-120">The input audio is paired against the provided group of speakers, and in the case that there is a match found, the speaker’s identity is returned.</span></span>

<span data-ttu-id="a44bd-121">All speakers should go through an enrollment process first to get their voice registered to the system, and have a voice print created.</span><span class="sxs-lookup"><span data-stu-id="a44bd-121">All speakers should go through an enrollment process first to get their voice registered to the system, and have a voice print created.</span></span>


### <a name="enrollment"></a><span data-ttu-id="a44bd-122">Enrollment</span><span class="sxs-lookup"><span data-stu-id="a44bd-122">Enrollment</span></span>

<span data-ttu-id="a44bd-123">Enrollment for speaker identification is text-independent, which means that there are no restrictions on what the speaker says in the audio.</span><span class="sxs-lookup"><span data-stu-id="a44bd-123">Enrollment for speaker identification is text-independent, which means that there are no restrictions on what the speaker says in the audio.</span></span> <span data-ttu-id="a44bd-124">The speaker's voice is recorded, and a number of features are extracted to form a unique voice signature.</span><span class="sxs-lookup"><span data-stu-id="a44bd-124">The speaker's voice is recorded, and a number of features are extracted to form a unique voice signature.</span></span> 


### <a name="recognition"></a><span data-ttu-id="a44bd-125">Recognition</span><span class="sxs-lookup"><span data-stu-id="a44bd-125">Recognition</span></span>

<span data-ttu-id="a44bd-126">The audio of the unknown speaker, together with the prospective group of speakers, is provided during recognition.</span><span class="sxs-lookup"><span data-stu-id="a44bd-126">The audio of the unknown speaker, together with the prospective group of speakers, is provided during recognition.</span></span> <span data-ttu-id="a44bd-127">The input voice is compared against all speakers in order to determine whose voice it is, and if there is a match found, the identity of the speaker is returned.</span><span class="sxs-lookup"><span data-stu-id="a44bd-127">The input voice is compared against all speakers in order to determine whose voice it is, and if there is a match found, the identity of the speaker is returned.</span></span>


<span data-ttu-id="a44bd-128">For more details about speaker identification, please refer to the API [Speaker - Identification](https://westus.dev.cognitive.microsoft.com/docs/services/563309b6778daf02acc0a508/operations/5645c068e597ed22ec38f42e).</span><span class="sxs-lookup"><span data-stu-id="a44bd-128">For more details about speaker identification, please refer to the API [Speaker - Identification](https://westus.dev.cognitive.microsoft.com/docs/services/563309b6778daf02acc0a508/operations/5645c068e597ed22ec38f42e).</span></span>
