---
title: 內容片段 — 設定瀏覽器（資產 — 內容片段）
description: 瞭解如何在設定瀏覽器中啟用內容片段功能。
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 17%

---

# 內容片段 — 設定瀏覽器{#content-fragments-configuration-browser}

瞭解如何在設定瀏覽器中啟用某些內容片段功能，以使用AEM強大的Headless傳送功能。

## 為您的執行個體啟用內容片段功能 {#enable-content-fragment-functionality-instance}

在使用內容片段之前，您必須使用 **設定瀏覽器** 若要啟用：

* **內容片段模型**  — 必要
* **GraphQL持續查詢**  — 選填

>[!CAUTION]
>
>如果您未啟用 **內容片段模型**：
>
>* 此 **建立** 選項無法用於建立模型。
>* 您無法 [選取Sites設定以建立相關的端點](/help/headless/graphql-api/graphql-endpoint.md).

若要啟用內容片段功能，您必須執行下列動作：

* 透過設定瀏覽器啟用內容片段功能
* 將設定套用至您的資產資料夾

### 在設定瀏覽器中啟用內容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

若要使用特定 [內容片段功能](#creating-a-content-fragment-model)，您 **必須** 首先透過 **設定瀏覽器**：

>[!NOTE]
>
>另請參閱 [設定瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser).

>[!NOTE]
>
>[子組態](/help/implementing/developing/introduction/configurations.md#configuration-resolution) （巢狀內嵌於其他設定的設定）完全支援與內容片段、內容片段模型和GraphQL查詢搭配使用。
>
>請注意：
>
>
>* 在子組態中建立模型後，無法將模型移動或複製到另一個子組態。
>
>* GraphQL端點（仍然）以父（根）設定為基礎。
>
>* 與父（根）設定相關的持續查詢（仍）已儲存。


1. 導覽至「 **工具**」、「 **一般**」，然後開啟「 **設定瀏覽器**」。

1. 使用 **建立** 若要開啟對話方塊，您可以：

   1. 指定 **標題**.
   1. **名稱**&#x200B;會成為存放庫中的節點名稱。
      * 它會根據標題自動產生，並根據 [AEM 命名慣例](/help/implementing/developing/introduction/naming-conventions.md)進行調整。
      * 您可以視需要加以調整。
   1. 若要啟用其使用，請選取
      * **內容片段模型**
      * **GraphQL 持續性查詢**

      ![定義設定](assets/cfm-conf-01.png)

1. 選取 **建立** 以儲存定義。

<!-- 1. Select the location appropriate to your website. -->

### 套用設定到資產資料夾 {#apply-the-configuration-to-your-assets-folder}

設定時 **全域** 已啟用內容片段功能，然後套用至任何資產資料夾。

若要搭配可比的「資產」資料夾使用其他設定（即不包括全域），您必須定義連線。 選取適當的連線即可完成此連線 **設定** 在 **Cloud Service** 的標籤 **資料夾屬性** 的對應資料夾。

![套用設定](assets/cfm-conf-02.png)
