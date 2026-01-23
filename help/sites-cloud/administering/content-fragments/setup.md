---
title: 內容片段 — 設定
description: 瞭解如何啟用內容片段和GraphQL的功能以搭配AEM Headless傳送功能和頁面編寫。
feature: Content Fragments
role: Developer
exl-id: 3974d698-1e7d-4a5f-a6d5-cbf8d96b4095
solution: Experience Manager Sites
source-git-commit: b3e1d3a3770531728d696be125f074881f179573
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 4%

---

# 內容片段 — 設定 {#content-fragments-setup}

Adobe Experience Manager (AEM) as a Cloud Service中的內容片段可讓您準備內容以用於多個位置和多個管道。 這非常適合於Headless傳送和頁面編寫。

要為內容片段功能啟用執行個體，您需要啟用：

* **內容片段模型** — 必要

  >[!CAUTION]
  >
  >如果未啟用&#x200B;**內容片段模型**：
  >
  >* **建立**&#x200B;選項將無法用於建立模型。
  >* 您將無法[選取Sites設定以建立相關的端點](/help/headless/graphql-api/graphql-endpoint.md)。

* **GraphQL持續查詢** — 選擇性

設定您的執行個體已完成：

* 由[在設定瀏覽器中啟用功能](#enable-content-fragment-functionality-configuration-browser)
* 然後[將設定套用至您的個別Assets資料夾](#apply-the-configuration-to-your-folder)

>[!TIP]
>
>內容片段可以[發佈至Edge Delivery Services。](https://www.aem.live/developer/content-fragment-overlay)

## 在設定瀏覽器中啟用內容片段功能 {#enable-content-fragment-functionality-configuration-browser}

若要使用內容片段功能、內容片段模型和GraphQL持續查詢，您&#x200B;**必須**&#x200B;先透過&#x200B;**設定瀏覽器**&#x200B;啟用它們：

>[!NOTE]
>
>如需詳細資訊，請參閱[設定瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)。

>[!NOTE]
>
>[子組態](/help/implementing/developing/introduction/configurations.md#configuration-resolution) （巢狀在另一個組態中的組態）完全支援與內容片段、內容片段模型和GraphQL查詢搭配使用。
>
>請注意：
>
>* 在子組態中建立模型後，無法將模型移動或複製到另一個子組態。
>
>* GraphQL端點將（仍然）以父（根）設定為基礎。
>
>* 將（仍）儲存與父（根）設定相關的持續查詢。

1. 導覽至「 **工具**」、「 **一般**」，然後開啟「 **設定瀏覽器**」。

1. 使用&#x200B;**建立**&#x200B;開啟對話方塊，您可以：

   1. 指定&#x200B;**標題**。
   1. 建立後，**Name**&#x200B;會成為存放庫中的節點名稱。
您可以輸入名稱。 如果您將欄位保留空白，欄位將根據標題自動產生，然後根據[AEM命名慣例](/help/implementing/developing/introduction/naming-conventions.md)進行調整；您可以視需要調整結果。
   1. 若要啟用其使用，請選取
      * **內容片段模型**
      * **GraphQL 持續性查詢**

      ![定義設定](assets/cf-setup-create-conf.png)

1. 選取&#x200B;**建立**&#x200B;以儲存定義。

## 將設定套用至資料夾 {#apply-the-configuration-to-your-folder}

為內容片段功能啟用設定&#x200B;**global**&#x200B;後，它會套用至任何Assets資料夾 — 可透過&#x200B;**Assets**&#x200B;主控台存取。

若要搭配可比的Assets資料夾使用其他設定（因此不包括全域），您必須定義連線。 請在適當資料夾的&#x200B;**資料夾屬性**&#x200B;的&#x200B;**雲端服務**&#x200B;索引標籤中，選取適當的&#x200B;**設定**&#x200B;來執行此動作。

![套用組態](assets/cf-setup-apply-conf.png)
