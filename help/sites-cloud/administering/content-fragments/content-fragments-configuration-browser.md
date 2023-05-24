---
title: 內容片段 — 設定瀏覽器
description: 瞭解如何在設定瀏覽器中啟用內容片段和GraphQL功能，以利用AEM Headless傳送功能。
feature: Content Fragments
role: User
exl-id: 55d442ae-ae06-4dfa-8e4e-b415385ccea5
source-git-commit: 34574fdc7f246499bd238fef388671d2287e62bc
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 26%

---

# 內容片段 — 設定瀏覽器{#content-fragments-configuration-browser}

瞭解如何在設定瀏覽器中啟用特定內容片段功能。

## 為您的執行個體啟用內容片段功能 {#enable-content-fragment-functionality-instance}

在使用內容片段之前，您需要使用 **設定瀏覽器** 若要啟用：

* **內容片段模型**  — 必要
* **GraphQL持續查詢**  — 選擇性

>[!CAUTION]
>
>如果您未啟用 **內容片段模型**：
>
>* 此 **建立** 選項將不可用於建立新模型。
>* 您將無法 [選取Sites設定以建立相關的端點](/help/headless/graphql-api/graphql-endpoint.md).


若要啟用內容片段功能，您需要：

* 透過設定瀏覽器啟用內容片段功能
* 將設定套用至您的資產資料夾

### 在設定瀏覽器中啟用內容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

至 [使用特定內容片段功能](#creating-a-content-fragment-model) 您 **必須** 首先透過 **設定瀏覽器**：

>[!NOTE]
>
>如需詳細資訊，另請參閱 [設定瀏覽器：](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[子設定](/help/implementing/developing/introduction/configurations.md#configuration-resolution) （巢狀內嵌於其他設定的設定）完全支援與內容片段、內容片段模型和GraphQL查詢搭配使用。
>
>請注意：
>
>
>* 在子組態中建立模型後，無法將模型移動或複製到另一個子組態。
>
>* GraphQL端點將（仍然）以父（根）設定為基礎。
>
>* 將（仍）儲存與父（根）設定相關的持續查詢。



1. 導覽至「 **工具**」、「 **一般**」，然後開啟「 **設定瀏覽器**」。

1. 使用 **建立** 若要開啟對話方塊，您可以：

   1. 指定 **標題**.
   1. **名稱**&#x200B;將成為存放庫中的節點名稱。
      * 它會根據標題自動產生，並根據[AEM 命名慣例](/help/implementing/developing/introduction/naming-conventions.md)進行調整
      * 您可以視需要加以調整。
   1. 若要啟用其使用，請選取
      * **內容片段模型**
      * **GraphQL 持續性查詢**

      ![定義設定](assets/cfm-conf-01.png)


1. 選取 **建立** 以儲存定義。

<!-- 1. Select the location appropriate to your website. -->

### 將設定套用至資料夾 {#apply-the-configuration-to-your-folder}

設定時 **全域** 已啟用內容片段功能，然後套用至任何資產資料夾 — 可透過存取 **資產** 主控台。

若要搭配可比的「資產」檔案夾使用其他設定 (例如排除全域)，您必須定義連線。若要這麼做，請在適當資 **料夾的「資料夾屬性** 」的「雲端服務 **」標籤** 中選取適當的「設定 **** 」。

![套用設定](assets/cfm-conf-02.png)
