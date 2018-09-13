---
title: Update your knowledge base with QnA Maker | Microsoft Docs
description: Use QnA Maker to update your knowledge base in a variety of ways.
services: cognitive-services
author: pchoudhari
manager: rsrikan
ms.service: cognitive-services
ms.technology: qnamaker
ms.topic: article
ms.date: 12/08/2016
ms.author: pchoudh
ms.openlocfilehash: 03b50d714ab4fbc135ab8f30a89259f911c27cfc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555543"
---
# <a name="update-your-knowledge-base"></a>Update your knowledge base
There are several ways you might want to update your knowledge base. Choose what is appropriate from the below methods.

## <a name="editorial-qna-updates"></a>Editorial QnA updates
Edit the QnA table directly. In addition, you can add/delete a QnA Pair, or add an alteration of an existing QnA pair. This is ideal for quick editorial fixes to your knowledge base

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/editKBTable.png)

To save your changes, press Save and retrain button.

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/kbSaveRetrain.png)

## <a name="update-the-sources"></a>Update the sources ##
If you need to update the sources of data of your knowledge base, go to the settings tab and update the sources.

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/kbSettings.png)

Once done with changes, click on Save and retrain

## <a name="download-and-upload"></a>Download and upload
There is also a way to replace your entire knowledge base at one go. This is ideal for bulk updates to your knowledge base. Upload KB expects file format of tab separated columns of Question, Answer and Source.

You have an option to download the entire knowledge base by clicking on Download Knowledge Base, make changes, and then upload the knowledge base.

>[!WARNING]
>Uploading a knowledge base overwrites the existing QnAs in the knowledge base.

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/kbDownloadLink.png)

To save your changes, press Save and retrain button.

![alt text](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/QnAMaker/Images/kbSaveRetrain.png)




