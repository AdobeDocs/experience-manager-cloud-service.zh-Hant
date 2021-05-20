---
title: 建立資產資料夾無頭快速入門手冊
description: 使用AEM內容片段模型來定義內容片段的結構，這是您無頭內容的基礎。
exl-id: 9a156a17-8403-40fc-9bd0-dd82fb7b2235
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# 建立資產資料夾無頭快速入門手冊{#creating-an-assets-folder}

使用AEM內容片段模型來定義內容片段的結構，這是您無頭內容的基礎。 內容片段接著會儲存在資產資料夾中。

##  什麼是資產資料夾？{#what-is-an-assets-folder}

[現在您已建立內容片段模](create-content-model.md) 型，定義您未來內容片段所需的結構，因此您可能很高興能建立一些片段。

不過，您首先需要建立資產資料夾，以便儲存這些資產。

資產資料夾可用來[組織傳統內容資產](/help/assets/manage-digital-assets.md)，例如影像和視訊，以及內容片段。

## 如何建立資產資料夾{#how-to-create-an-assets-folder}

管理員只需偶爾建立資料夾，即可在建立內容時加以組織。 在本快速入門手冊中，我們只需建立一個資料夾。

1. 以Cloud Service身分登入AEM，然後在主功能表中選取&#x200B;**導覽 — >資產 — >檔案**。
1. 點選或按一下&#x200B;**建立 — >資料夾**。
1. 為資料夾提供&#x200B;**Title**&#x200B;和&#x200B;**名稱**。
   * **Title**&#x200B;應是描述性的。
   * **Name**&#x200B;將成為儲存庫中的節點名稱。
      * 系統會根據標題自動產生，並根據[AEM命名慣例進行調整。](/help/implementing/developing/introduction/naming-conventions.md)
      * 如有需要，可加以調整。

   ![建立資料夾](../assets/assets-folder-create.png)
1. 選擇剛建立的資料夾，然後從工具欄中選擇&#x200B;**屬性**（或使用`p` [鍵盤快捷鍵。](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)）
1. 在&#x200B;**屬性**&#x200B;窗口中，選擇&#x200B;**Cloud Services**&#x200B;頁簽。
1. 對於&#x200B;**雲配置**&#x200B;選擇您先前建立的[配置。](create-configuration.md)

   ![設定資產資料夾](../assets/assets-folder-configure.png)
1. 點選或按一下「**儲存並關閉**」。
1. 點選或按一下確認視窗中的&#x200B;**確定**。

   ![確認窗口](../assets/assets-folder-confirmation.png)

您可以在剛建立的資料夾中建立其他子資料夾。 子資料夾將繼承父資料夾的&#x200B;**雲配置**。 但是，如果您想使用其他配置的模型，則可以覆蓋此項。

如果您使用本地化的網站結構，則可以在新資料夾下建立語言根](/help/assets/translate-assets.md)。[

## 後續步驟{#next-steps}

現在您已為內容片段建立資料夾，您可以繼續前往快速入門手冊的第四部分，並[建立內容片段。](create-content-fragment.md)

>[!TIP]
>
>如需管理內容片段的完整詳細資訊，請參閱[內容片段檔案](/help/assets/content-fragments/content-fragments.md)
