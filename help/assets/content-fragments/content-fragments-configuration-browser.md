---
title: 內容片段——設定瀏覽器
description: 瞭解如何在設定瀏覽器中啟用特定內容片段功能。
translation-type: tm+mt
source-git-commit: ae918d074d4bacfc207d4dca2c67f41a3118aff4
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 20%

---


# 內容片段——設定瀏覽器{#content-fragments-configuration-browser}

>[!CAUTION]
>
>AEM GraphQL API（針對內容片段傳送）將於2021年初發行。
>
>相關檔案已可供預覽使用。

## 啟用實例{#enable-content-fragment-functionality-instance}的內容片段功能

使用內容片段之前，您需要使用&#x200B;**Configuration Browser**&#x200B;來啟用：

* **內容片段模型** -強制
* **GraphQL持久查詢** -可選

>[!CAUTION]
>
>如果未啟用「內容片段模型」****，則「建立」**選項將不可用於建立新模型。**

若要啟用內容片段功能，您需要：

* 透過設定瀏覽器啟用內容片段功能
* 將設定套用至您的「資產」檔案夾

### 在配置瀏覽器{#enable-content-fragment-functionality-in-configuration-browser}中啟用內容片段功能

要使用某些內容片段功能](#creating-a-content-fragment-model),**必須**&#x200B;首先通過&#x200B;**配置瀏覽器**&#x200B;啟用它們：[

>[!NOTE]
>
>如需詳細資訊，請參閱[組態瀏覽器：](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)。

1. 導覽至「 **工具**」、「 **一般**」，然後開啟「 **設定瀏覽器**」。
2. 選擇適合您網站的位置。
3. 使用&#x200B;**Create**&#x200B;開啟對話方塊，您可在其中：

   1. 指定&#x200B;**Title**。
   2. 若要啟用其使用選擇
      * **內容片段模型**
      * **GraphQL持久查詢**

      ![定義配置](assets/cfm-conf-01.png)


4. 選擇&#x200B;**建立**&#x200B;以保存定義。

### 將設定套用至您的資產資料夾{#apply-the-configuration-to-your-assets-folder}

當設定&#x200B;**global**&#x200B;啟用內容片段功能時，則會套用至任何「資產」檔案夾。

若要搭配可比的「資產」檔案夾使用其他設定 (例如排除全域)，您必須定義連線。若要這麼做，請在適當資 **料夾的「資料夾屬性** 」的「雲端服務 **」標籤** 中選取適當的「設定 **** 」。

![套用設定](assets/cfm-conf-02.png)