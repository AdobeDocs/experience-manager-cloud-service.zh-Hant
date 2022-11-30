---
title: 建立應用程式的內容結構
description: 了解如何使用AEM內容片段模型，建立可作為所有無頭內容基礎的結構。
hidefromtoc: true
index: false
source-git-commit: 6010fb398ec8c04ae9153f313585bcf38ccaa26d
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---


# 建立應用程式的內容結構 {#content-structure}

內容片段可讓您設計、建立、組織和發佈不受頁面影響的內容。 使用它們，您可以準備可在多個位置和多個頻道上使用的內容，非常適合無頭傳送。 內容片段模型可用來定義此內容的結構，且是您管理無頭內容所需的第一件事。

為協助您了解如何完成此作業，此AEM Trials模組會透過快速互動導覽，引導您完成程式，先建立模型，然後新增其結構。 本檔案是產品內導覽的補充，涵蓋相同步驟，並視情況連結至其他資源。

## 內容片段模型主控台 {#content-fragment-model-console}

您可以在內容片段模型控制台上啟動。 內容片段模型主控台可視為模型庫。 您可使用主控台建立新模型並管理現有模型。 您的主控台會啟動空白，因此我們建立新模型！

![內容片段模型主控台](assets/content-structure/content-fragment-model-console.png)

如果您想自行導覽至應用程式內指引以外的內容片段模型主控台，請使用頁面左上角的Adobe圖示找到。 這會開啟AEM的全域導覽。 從這裡，您選擇 **工具** 標籤，然後 **一般** -> **內容片段模型**.

>[!TIP]
>
>如果您想進一步了解AEM中的導覽，請參閱 [「其他資源」部分](#additional-resources) ，以取得AEM基本處理的詳細資訊。

## 建立模型 {#create-model}

進入內容片段模型控制台後，您可以建立新模型來代表您自己的無頭內容。

1. 在內容片段模型控制台中，按一下 **建立** 按鈕，開始建立內容片段模型。

1. 「建立模型」精靈會啟動，引導您建立內容片段模型。

   ![內容片段模型精靈](assets/content-structure/model-wizard.png)

   提供必填資訊。

   * **模型標題**  — 這是模型的簡要描述，通常指明其目的。
   * **啟用模型**  — 預設會核取此選項，且必須勾選此選項，才能稍後根據此模型建立內容片段。

   您也可以選擇新增更長時間 **說明** 和 **標籤** 以便日後在內容片段模型主控台中對其分類並區別給您的使用者。

   >[!TIP]
   >
   >如果您對標籤如何組織內容感興趣，請參閱 [「其他資源」部分](#additional-resources) ，以取得AEM中標籤的詳細資訊。

1. 填入必填欄位後，按一下 **建立** ，以建立模型。

1. 此 **成功** 對話框確認已建立模型。

   ![建立新內容片段模型的成功對話方塊](assets/content-structure/success.png)

1. 在可以使用模型之前，還需要定義其資料的結構。 按一下 **開啟** 在對話框中開啟它，然後繼續定義模型。

## 向模型添加欄位 {#configure-model}

內容片段模型本質上是內容片段的結構。 即定義模型包含的欄位/資料類型。

![內容片段模型編輯器](assets/content-structure/model-editor.png)

使用內容片段模型編輯器，您可以使用拖放介面來定義內容片段模型的欄位。

1. 從拖曳欄位 **資料類型** 面板，並將其拖放至您的內容片段模型。 有多種資料類型可供選擇，例如單行文字、多行文字、編號，以及其他片段的參考。

   ![新增資料類型](assets/content-structure/drop-fields.png)

   >[!TIP]
   >
   >如果您想要取得可用資料類型的詳細資訊，請參閱 [「其他資源」部分](#additional-resources) ，取得詳細內容片段模型檔案。

1. 放置資料類型後， **資料類型** 欄自動變更為 **屬性** 索引標籤，您可在此定義剛放置的資料類型的詳細資料。

   ![資料欄位的「屬性」索引標籤](assets/content-structure/data-type-properties.png)

   模型的屬性可以包括欄位名稱、欄位類型、欄位長度（如果是強制欄位）等。

1. 使用 **屬性** 索引標籤來定義屬性，例如預設值、最大長度（如果是必要欄位）等。

   >[!TIP]
   >
   >如果您想要取得可用屬性的詳細資訊，請參閱 [「其他資源」部分](#additional-resources) ，取得詳細內容片段模型檔案。

1. 新增內容片段模型所需的所有欄位後，按一下 **儲存** 窗口的右上角。

1. 這會儲存模型，並將您傳回「內容片段模型控制台」，您可在其中新增更多模型。

![模組完成](assets/content-structure/content-fragment-model-console-populated.png)

## 您已學習如何建立內容片段模型 {#conclusion}

在本模組中，您學習了如何建立內容片段模型來表示無頭資料的結構。 首先，您建立了模型，然後以資料類型及其相關屬性填入模型，借此定義無頭內容的架構。

現在您有了自己的內容片段模型，可以使用模型來建立內容片段。 模組 [建立新內容](create-content.md) 詳細資訊，以使用新的內容片段模型來建立無標題內容。

您可以按一下，返回試用主螢幕 **解決方案** 按鈕，然後選擇 **Experience Manager**.

![導覽首頁](assets/content-structure/home.png)

## 其他資源 {#additional-resources}

如需內容片段和AEM的詳細資訊，請考慮檢閱此額外檔案。

* [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 如何為新使用者導覽和使用AEM的檔案
* [使用標籤](/help/sites-cloud/authoring/features/tags.md)  — 如何使用AEM中的標籤來組織內容的檔案
* [內容片段](/help/assets/content-fragments/content-fragments.md)  — 內容片段的概觀和內容片段完整檔案的連結
* [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)  — 內容片段模型的完整檔案
* [內容片段模型 — 資料類型](/help/assets/content-fragments/content-fragments-models.md#data-types)  — 內容片段模型可用各種資料類型的詳細資訊
* [內容片段模型 — 屬性](/help/assets/content-fragments/content-fragments-models.md#data-types)  — 內容片段模型資料類型可用各種屬性的詳細資訊
