---
title: 內容片段 — 配置瀏覽器（資產 — 內容片段）
description: 瞭解如何在配置瀏覽器中啟用內容片段功能。
exl-id: 9fc911de-1d33-4811-8f58-ea21ce94bedb
source-git-commit: 34574fdc7f246499bd238fef388671d2287e62bc
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 28%

---

# 內容片段 — 配置瀏覽器{#content-fragments-configuration-browser}

瞭解如何在配置瀏覽器中啟用某些內容片段功能，以利用功AEM能強大的無頭傳送功能。

## 為您的執行個體啟用內容片段功能 {#enable-content-fragment-functionality-instance}

在使用內容片段之前，您需要使用 **配置瀏覽器** 啟用：

* **內容片段模型**  — 強制
* **GraphQL永續查詢**  — 可選

>[!CAUTION]
>
>如果未啟用 **內容片段模型**:
>
>* 這樣 **建立** 的子菜單。
>* 你將無法 [選擇「站點」配置以建立相關端點](/help/headless/graphql-api/graphql-endpoint.md)。


要啟用內容片段功能，您需要：

* 通過配置瀏覽器啟用內容片段功能
* 將配置應用到Assets資料夾

### 在設定瀏覽器中啟用內容片段功能 {#enable-content-fragment-functionality-in-configuration-browser}

至 [使用某些內容片段功能](#creating-a-content-fragment-model) 你 **必須** 首先通過 **配置瀏覽器**:

>[!NOTE]
>
>有關詳細資訊，請參閱 [配置瀏覽器：](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)。

>[!NOTE]
>
>[子配置](/help/implementing/developing/introduction/configurations.md#configuration-resolution) （嵌套在另一配置中的配置）完全支援用於內容片段、內容片段模型和GraphQL查詢。
>
>只要注意：
>
>
>* 在子配置中建立模型後，不能將模型移動或複製到另一個子配置。
>
>* GraphQL終結點將（仍然）基於父（根）配置。
>
>* 保留的查詢將（仍然）保存為與父（根）配置相關。



1. 導覽至「 **工具**」、「 **一般**」，然後開啟「 **設定瀏覽器**」。

1. 使用 **建立** 開啟對話框，在其中：

   1. 指定 **標題**。
   1. **名稱**&#x200B;將成為存放庫中的節點名稱。
      * 它會根據標題自動產生，並根據[AEM 命名慣例](/help/implementing/developing/introduction/naming-conventions.md)進行調整
      * 如有必要，您可以調整它。
   1. 要啟用其使用，請選擇
      * **內容片段模型**
      * **GraphQL 持續性查詢**

      ![定義設定](assets/cfm-conf-01.png)


1. 選擇 **建立** 的子菜單。

<!-- 1. Select the location appropriate to your website. -->

### 套用設定到資產資料夾 {#apply-the-configuration-to-your-assets-folder}

當配置 **全球** 為內容片段功能啟用，然後應用於任何「資產」資料夾。

若要搭配可比的「資產」檔案夾使用其他設定 (例如排除全域)，您必須定義連線。若要這麼做，請在適當資 **料夾的「資料夾屬性** 」的「雲端服務 **」標籤** 中選取適當的「設定 **** 」。

![應用配置](assets/cfm-conf-02.png)
