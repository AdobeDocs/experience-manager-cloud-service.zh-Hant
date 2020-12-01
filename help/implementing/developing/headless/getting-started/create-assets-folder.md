---
title: 建立資產資料夾無頭快速入門手冊
description: 內容片段模型定義內容片段的結構。 內容片段接著會儲存在資產檔案夾中。
translation-type: tm+mt
source-git-commit: 9c801af38142434a5a0302b73b6fc1469a0eaab2
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---


# 《 Creating an Assets Folder Headless Quick Start Guide》（建立資產資料夾無頭快速入門手冊）{#creating-an-assets-folder}

內容片段模型定義內容片段的結構。 內容片段接著會儲存在資產檔案夾中。

##  什麼是資產資料夾？{#what-is-an-assets-folder}

[現在您已建立內容片段模型，](create-content-model.md) 定義您未來內容片段的結構，您可能很高興能建立一些片段。

不過，您必須先建立資產檔案夾，以儲存資產檔案夾。

資產資料夾用於[組織傳統內容資產](/help/assets/manage-digital-assets.md)，例如影像和視訊以及內容片段。

## 如何建立資產資料夾{#how-to-create-an-assets-folder}

管理員只需要偶爾建立資料夾，即可在建立內容時加以組織。 為了本快速入門手冊的目的，我們只需要建立一個資料夾。

1. 以雲端服務的身分登入AEM，並從主功能表選取「**導覽->資產->檔案**」。
1. 點選或按一下「建立->資料夾&#x200B;**」。**
1. 為資料夾提供&#x200B;**Title**&#x200B;和&#x200B;**Name**。
   * **Title**&#x200B;應為描述性。
   * **Name**&#x200B;將成為儲存庫中的節點名。
      * 系統會根據標題自動產生，並根據[AEM命名慣例進行調整。](/help/implementing/developing/introduction/naming-conventions.md)
      * 如有需要，可加以調整。

   ![建立資料夾](../assets/assets-folder-create.png)
1. 選擇剛建立的資料夾，然後從工具欄中選擇&#x200B;**屬性**（或使用`p` [鍵盤快捷鍵。](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)）
1. 在&#x200B;**屬性**&#x200B;視窗中，選取&#x200B;**雲端服務**&#x200B;標籤。
1. 對於&#x200B;**雲配置**&#x200B;選擇您先前建立的[配置。](create-configuration.md)

   ![設定資產資料夾](../assets/assets-folder-configure.png)
1. 點選或按一下「儲存並關閉」**。**
1. 在確認窗口中點選或按一下&#x200B;**確定**。

   ![確認窗口](../assets/assets-folder-confirmation.png)

您可以在剛建立的檔案夾中建立其他子檔案夾。 子資料夾將繼承父資料夾的&#x200B;**Cloud Configuration**。 不過，如果希望使用其他配置的模型，則可以覆蓋此選項。

如果您使用本地化的網站結構，您可以在新資料夾下建立[語言根](/help/assets/translate-assets.md)。

## 後續步驟{#next-steps}

現在，您已為「內容片段」建立資料夾，您可以移至快速入門手冊的第四部份，並[建立內容片段。](create-content-fragment.md)

>!![TIP]
如需管理內容片段的完整詳細資訊，請參閱[內容片段檔案](/help/assets/content-fragments/content-fragments.md)
