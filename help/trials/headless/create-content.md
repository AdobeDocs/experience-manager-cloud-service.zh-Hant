---
title: 建立無頭內容
description: 使用您先前建立的內容片段模型來建立可用於頁面編寫的內容，或作為無頭內容的基礎。
hidefromtoc: true
index: false
source-git-commit: 7d5161d97a93d4731e33eda586179560a6a55ef3
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 0%

---


# 建立無頭內容 {#create-content}

遵循產品內學習模組，了解如何使用 [您先前建立的內容片段模型](content-structure.md) 來建立可用於頁面製作的內容，或作為無頭內容的基礎。 本檔案是互動式導覽的補充，涵蓋相同步驟，並視需要連結至其他資源。

## 內容片段 {#introduction}

在AEMas a Cloud Service中，內容片段是根據內容片段模型所定義的結構而組成的無頭內容片段。 您可以從「內容片段」主控台開始，建立您自己的內容片段。 內容片段主控台可視為無頭內容的程式庫。 您可以使用主控台建立新內容片段，並管理現有片段。 您的主控台會啟動空白，因此我們要建立新片段！

![編輯片段的內容](assets/create-content/content-fragment-console.png)

如果您想自行導覽至應用程式內指引以外的內容片段主控台，請使用頁面左上角的Adobe圖示找到。 這會開啟AEM的全域導覽。 從這裡，您選擇 **導覽** 標籤，然後 **內容片段**.

>[!TIP]
>
>如果您想進一步了解AEM中的導覽，請參閱 [「其他資源」部分](#additional-resources) ，以取得AEM基本處理的詳細資訊。

## 建立內容片段 {#create-fragment}

內容片段代表您的無頭內容。 但只能根據預先定義的內容結構來建立。 您先前建立的內容片段模型可作為該結構。

1. 點選或按一下 **建立** 按鈕，開啟 **新內容片段** 對話方塊，以開始建立新內容片段。

   ![建立內容片段對話方塊](assets/create-content/create-content-fragment.png)

1. 如果您遵循應用程式內指引， **位置** 會自動填入。

   1. 如果您未遵循指南，請使用路徑瀏覽器來選取專案資料夾。

   1. 在 **新內容片段** 對話框，點選或按一下 **選擇位置** 按鈕（看起來像資料夾的圖示） **位置** 欄位。

      ![選擇位置對話框](assets/create-content/choose-location.png)
   * 或者，在按一下前，在內容片段控制台的左側導覽面板中選取路徑 **建立**.


1. 在 **內容片段模型** 下拉式清單中，從下拉式清單中選取您先前建立的內容片段模型。

1. 新增 **標題** （針對內容片段）。

1. 點選或按一下 **建立和開啟**.

## 內容片段編輯器 {#edit-fragment}

儲存新內容片段後，內容片段編輯器隨即開啟，您可在其中提供片段的實際內容。

1. 編輯器顯示在所選模型中定義的欄位。 您可以在此編輯它們以完成內容片段。 系統會自動儲存您的進度。

   ![內容片段編輯器](assets/create-content/content-fragment-editor.png)

1. 如果內容片段的模型有許多欄位，您可以使用 **變數** 面板。 系統會在此處標籤有錯誤的欄位。

1. 為了讓內容片段可供外部應用程式使用，您需要發佈它。 點選或按一下 **發佈** 按鈕。

1. 選擇 **現在** 從下拉式清單中。 您也可以排程在稍後發佈。

   ![發佈按鈕](assets/create-content/publish.png)

   >[!TIP]
   >
   >如果您想要進一步了解在AEM中發佈內容，請參閱 [「其他資源」部分](#additional-resources) ，以取得有關發佈的詳細資訊。

1. AEM會自動執行參考檢查，以確定已針對您的內容片段發佈所有必要資源。 在此情況下，您也需要發佈您建立的模型。 點選或按一下 **發佈**.

   ![參考檢查](assets/create-content/references.png)

1. 出版物在橫幅中確認。

   ![發佈確認](assets/create-content/publish-confirm.png)

## 您已學習如何建立內容片段！ {#conclusion}

在本模組中，您學習了如何根據您先前建立的模型建立內容片段。 這是內容作者建立結構化無頭內容的方式。

現在您的內容已建立並發佈，您可以透過AEM API透過Graph QL擷取該內容。 您將在模組中了解此資訊 [透過GraphQL API擷取內容。](extract-content.md)

您可以按一下，返回試用主螢幕 **解決方案** 按鈕，然後選擇 **Experience Manager**.

![導覽首頁](assets/create-content/home.png)

## 其他資源 {#additional-resources}

如需內容片段和AEM的詳細資訊，請考慮檢閱此額外檔案。

* [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 如何為新使用者導覽和使用AEM的檔案
* [管理內容片段 — 發佈和參考](/help/assets/content-fragments/content-fragments-managing.md#publishing-and-referencing-a-fragment)  — 如何在AEM中發佈內容的詳細資訊
* [內容片段](/help/assets/content-fragments/content-fragments.md)  — 內容片段的概觀和內容片段完整檔案的連結
* [管理內容片段](/help/assets/content-fragments/content-fragments-managing.md)  — 如何建立和管理內容片段
