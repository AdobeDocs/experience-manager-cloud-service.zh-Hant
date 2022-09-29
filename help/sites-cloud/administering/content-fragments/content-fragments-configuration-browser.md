---
title: 內容片段 — 設定瀏覽器
description: 了解如何在設定瀏覽器中啟用內容片段和GraphQL功能，以運用AEM無周邊傳送功能。
feature: Content Fragments
role: User
exl-id: 55d442ae-ae06-4dfa-8e4e-b415385ccea5
source-git-commit: 944665bc7cac1f00811187a508a18800c3d73f2a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 14%

---

# 內容片段 — 設定瀏覽器{#content-fragments-configuration-browser}

了解如何在設定瀏覽器中啟用特定內容片段功能。

## 為您的執行個體啟用內容片段功能 {#enable-content-fragment-functionality-instance}

使用內容片段之前，您需要使用 **配置瀏覽器** 啟用：

* **內容片段模型** 必填
* **GraphQL持續查詢**  — 可選

>[!CAUTION]
>
>如果您未啟用 **內容片段模型**:
>
>* the **建立** 建立新模型時將無法使用選項。
>* 你將無法 [選擇Sites配置以建立相關端點](/help/headless/graphql-api/graphql-endpoint.md).


若要啟用內容片段功能，您需要：

* 透過設定瀏覽器啟用內容片段功能的使用
* 將設定套用至資產資料夾

### 在設定瀏覽器中啟用內容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

結束日期 [使用特定內容片段功能](#creating-a-content-fragment-model) you **必須** 首先透過 **配置瀏覽器**:

>[!NOTE]
>
>如需詳細資訊，另請參閱 [配置瀏覽器：](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[子配置](/help/implementing/developing/introduction/configurations.md#configuration-resolution) 完全支援搭配內容片段、內容片段模型和GraphQL查詢使用（巢狀配置內的配置）。
>
>請注意：
>
>
>* 在子配置中建立模型後，不可將模型移動或複製到另一個子配置。
>
>* GraphQL端點將（仍然）基於父（根）配置。
>
>* 保存的查詢將（仍）與父（根）配置相關地保存。



1. 導覽至「 **工具**」、「 **一般**」，然後開啟「 **設定瀏覽器**」。

1. 使用 **建立** 開啟對話框，其中：

   1. 指定 **標題**.
   1. 此 **名稱** 會成為存放庫中的節點名稱。
      * 根據標題自動產生並根據 [AEM命名慣例。](/help/implementing/developing/introduction/naming-conventions.md)
      * 您可以視需要加以調整。
   1. 啟用其使用選擇
      * **內容片段模型**
      * **GraphQL持續查詢**

      ![定義配置](assets/cfm-conf-01.png)


1. 選擇 **建立** 以儲存定義。

<!-- 1. Select the location appropriate to your website. -->

### 將設定套用至資料夾 {#apply-the-configuration-to-your-folder}

設定時 **全球** 已啟用內容片段功能，則此功能會套用至任何可透過存取的資產資料夾 **資產** 控制台。

若要搭配可比的「資產」檔案夾使用其他設定 (例如排除全域)，您必須定義連線。若要這麼做，請在適當資 **料夾的「資料夾屬性** 」的「雲端服務 **」標籤** 中選取適當的「設定 **** 」。

![套用設定](assets/cfm-conf-02.png)
