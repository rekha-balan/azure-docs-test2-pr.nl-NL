---
title: Create a custom wake word
description: Learn how to create a custom wake word for the Speech Devices SDK.
titleSuffix: Azure Cognitive Services
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.technology: speech
ms.topic: article
ms.date: 04/28/2018
ms.author: v-jerkin
ms.openlocfilehash: e1a74828213b595e6955a750904de7a3c2a5a865
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869513"
---
# <a name="create-a-custom-wake-word-by-using-the-speech-service"></a>Create a custom wake word by using the Speech service

Your device is always listening for a wake word (or phrase). For example, "Hey Cortana" is a wake word for the Cortana assistant. When the user says the wake word, the device sends all subsequent audio to the cloud, until the user stops speaking. Customizing your wake word is an effective way to differentiate your device and strengthen your branding.

In this article, you learn how to create a custom wake word for your device.

## <a name="choose-an-effective-wake-word"></a>Choose an effective wake word

Consider the following guidelines when you choose a wake word:

* Your wake word should be an English word or a phrase. It should take no longer than two seconds to say.

* Words of 4 to 7 syllables work best. For example, "Hey, Computer" is a good wake word. Just "Hey" is a poor one.

* Wake words should follow common English pronunciation rules.

* A unique or even a made-up word that follows common English pronunciation rules might reduce false positives. For example, "computerama" might be a good wake word.

* Do not choose a common word. For example, "eat" and "go" are words that people say frequently in ordinary conversation. They might be false triggers for your device.

* Avoid using a wake word that might have alternative pronunciations. Users would have to know the "right" pronunciation to get their device to respond. For example, "509" can be pronounced "five zero nine," "five oh nine," or "five hundred and nine." "R.E.I." can be pronounced "r-e-i" or "ray." "Live" can be pronounced "/līv/" or "/liv/".

* Do not use special characters, symbols, or digits. For example, "Go#" and "20 + cats" would not be good wake words. However, "go sharp" or "twenty plus cats" might work. You can still use the symbols in your branding and use marketing and documentation to reinforce the proper pronunciation.

> [!NOTE]
> If you choose a trademarked word as your wake word, be sure that you own that trademark or that you have permission from the trademark owner to use the word. Microsoft is not liable for any legal issues that might arise from your choice of wake word.

## <a name="create-your-wake-word"></a>Create your wake word

Before you can use a custom wake word with your device, you must create the wake word by using the Microsoft Custom Wake Word Generation service. After you provide a wake word, the service produces a file that you deploy to your development kit to enable your wake word on your device.

1. Go to the [Custom Speech service portal](https://cris.ai/).

2. Create a new account with the email address at which you received the invitation for Azure Active Directory. 

    ![Create a new account](media/speech-devices-sdk/wake-word-1.png)
 
3.  After you sign in, fill out the form, and then select **Start my journey**.

    ![Successfully signed in](media/speech-devices-sdk/wake-word-3.png)
 
4. The **Custom Wake Word** page is not available to the public, so there is no link that takes you there. Select or paste in this link instead: https://cris.ai/customkws.

    ![The Custom Wake Word page is hidden](media/speech-devices-sdk/wake-word-4.png)
 
6. Type in the wake word of your choice, and then select **Submit the word**.

    ![Enter your wake word](media/speech-devices-sdk/wake-word-5.png)
 
7. It might take a few minutes for the files to be generated. You should see a spinning circle in your browser window. After a moment, an information bar appears, asking you to download a .zip file.

    ![Receiving the .zip file](media/speech-devices-sdk/wake-word-6.png)

8. Save the .zip file to your computer. You need this file to deploy the custom wake word to the development kit. To deploy the custom wake word, follow the instructions in [Get started with the Speech Devices SDK](speech-devices-sdk-qsg.md).

9. Select **Sign out.**

## <a name="next-steps"></a>Next steps

To get started, get a [free Azure account](https://azure.microsoft.com/free/) and sign up for the Speech Devices SDK.

> [!div class="nextstepaction"]
> [Sign up for the Speech Devices SDK](get-speech-devices-sdk.md)
