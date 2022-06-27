---
title: 配置Workfront和Experience Manager Assets之間的資產元資料映射
description: 在Adobe Workfront和Experience Manageras a Cloud Service應用程式之間映射資產元資料欄位。 映射元資料欄位的結果是，當您將資產從Workfront發送到Experience Manager Assets時，您可以在Experience Manager Assets查看映射的資產元資料。
source-git-commit: 212ecb5330de739b2e479d36462953ce33697c1c
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 0%

---

# 配置Adobe Workfront和Experience Manager Assets之間的資產元資料映射 {#asset-metadata-mapping-workfront-aem-assets}

您可以在Adobe Workfront和Experience Manageras a Cloud Service應用程式之間映射資產元資料欄位。 映射元資料欄位的結果是，當您將資產從Workfront發送到Experience Manager Assets時，您可以在Experience Manager Assets查看映射的資產元資料。

例如，在將影像發送到Experience Manager Assets時，如果需要保留影像的元資料欄位，如名稱、說明及其所屬項目在Workfront，請配置這些欄位並將其映射到Experience Manager Assets屬性。

**使用案例**

影像 `add-users-workfront.png` 存在於 `Metadata Syncs` 項目在Adobe Workfront。 您需要將該映像用以下元資料發送到Experience Manager Assetsas a Cloud Service:

* 專案名稱

* 文檔名稱

* 文檔說明

## 必備條件 {#prerequisites}

* 管理員對Workfront和Experience Manager Assetsas a Cloud Service應用程式的訪問權限。

* 整合 [Workfront和Experience Manager Assetsas a Cloud Service應用](https://one.workfront.com/s/document-item?bundleId=the-new-workfront-experience&amp;topicId=Content%2FDocuments%2FAdobe_Workfront_for_Experience_Manager_Assets_Essentials%2Fsetup-asset-essentials.htm&amp;_LANG=enus)。

## 在Workfront設定元資料映射 {#set-up-metadata-mapping}

要為Workfront的「項目名稱」、「文檔名稱」和「文檔說明」欄位設定元資料映射：

1. 按一下「主菜單」表徵圖 ![顯示菜單](assets/show-menu.svg) 位於Adobe Workfront應用程式的右上角，然後按一下 **[!UICONTROL 設定]**。

1. 選擇 **[!UICONTROL 文檔]** 在左面板中，選擇 **[!UICONTROL Experience Manager Assets]**。

1. 選擇Experience Manager Assets整合併按一下 **[!UICONTROL 編輯]**。

1. 按一下 **[!UICONTROL 元資料]**。 在 **[!UICONTROL 資產]** 的子菜單。 [!UICONTROL 項目] > [!UICONTROL 名稱] Workfront球場 `wm:projectName` Experience Manager Assets球場。 如果找不到確切的匹配項，Adobe建議尋找最佳匹配項，以繪製Workfront和Experience Manager Assets欄位。 可以避免映射不同資料類型的欄位。 例如，將日期Workfront欄位映射到說明「資產」欄位。
1. 映射 [!UICONTROL 文檔] > [!UICONTROL 名稱] Workfront球場 `wm:documentName` Experience Manager Assets球場。

   ![Workfront地圖](assets/workfront-metadata-mapping.png)

1. 映射 [!UICONTROL 文檔] > [!UICONTROL 說明] Workfront球場 `dc:description` Experience Manager Assets球場。

   >[!VIDEO](https://video.tv.adobe.com/v/344255)

## 將圖片從Workfront發送到Experience Manager Assets {#send-image-workfront-assets}

要將影像從Workfront發送到Experience Manager Assets:

1. 按一下「主菜單」表徵圖 ![顯示菜單](assets/show-menu.svg) 位於Adobe Workfront應用程式的右上角，然後按一下 **[!UICONTROL 項目]**。

1. 按一下 **[!UICONTROL 新建項目]** 來修改標籤元素的屬性。

1. 按一下 **[!UICONTROL 文檔]** 選項，拖動並選擇需要發送到Experience Manager Assets的影像。

1. 按一下 **[!UICONTROL 發送到]**，然後選擇「Experience Manager Assets軟體包」整合名稱。

   ![發送至AEM](assets/send-to-aem.png)

1. 選擇資產的目標資料夾，然後按一下 **[!UICONTROL 選擇資料夾]**。

1. 按一下「**[!UICONTROL 儲存]**」。

## 在Experience Manageras a Cloud Service中配置資產元資料映射 {#metadata-mapping-aem}

之後 [在Adobe Workfront配置資產元資料映射](#set-up-metadata-mapping)，必須在Experience Manager Assetsas a Cloud Service應用程式中使用相同的映射來顯示影像的相應元資料結果。

元資料映射是使用Experience Manager Assets的元資料架構執行的。 可以編輯新添加的或現有的元資料架構表單。 元資料架構表單包含頁籤和制表符內的表單項。 您可以將這些表單項映射到/配置到CRX儲存庫的元資料節點中的欄位。 可以將頁籤或表單項添加到元資料架構表單中。 有關詳細資訊，請參見 [元資料架構](metadata-schemas.md)。

要在Experience Manager Assetsas a Cloud Service中使用新的元資料表單配置元資料映射，請執行以下操作：

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 元資料架構]**。

1. 按一下 **[!UICONTROL 建立]** 的子菜單。 在對話框中，提供架構表單的標題，然後按一下 **[!UICONTROL 建立]** 的子菜單。

1. 選擇架構表單並按一下 **[!UICONTROL 編輯]**。

1. （可選）在元資料架構表單編輯器上，按一下 `+` 的子菜單。

1. 按一下 **[!UICONTROL 生成窗體]** 頁籤並拖動 **[!UICONTROL 單行文本]** 的子菜單。 按一下窗體中的元件。 在 **[!UICONTROL 生成窗體]** 頁籤：

   1. 指定 `Project Name` 的 **[!UICONTROL 欄位標籤]** 的子菜單。

   1. 指定 `./jcr:content/metadata/wm:projectName` 的 **[!UICONTROL 映射到屬性]** 的子菜單。 作為指導，請使用以下模板來定義「體驗管理器資產」中的欄位映射：
      `./jcr:content/metadata/<mapping defined for the field in workfront>`。

      在Workfront配置映射時，已映射 `wm:projectName` Experience Manager Assets欄位到項目>命名Workfront欄位。

      `wm` 引用命名空間名稱和 `projectName` 引用屬性標題。 使用 `namespace:propertyTitle` 格式以定義元資料欄位映射。

      ![發送至AEM](assets/metadata-schema-mapping.png)

1. 按一下 **[!UICONTROL 生成窗體]** 頁籤並拖動 **[!UICONTROL 單行文本]** 的子菜單。 按一下窗體中的元件。 在 **[!UICONTROL 生成窗體]** 頁籤：

   1. 指定 `Document Name` 的 **[!UICONTROL 欄位標籤]** 的子菜單。

   1. 指定 `./jcr:content/metadata/wm:documentName` 的 **[!UICONTROL 映射到屬性]** 的子菜單。
在Workfront配置映射時，已映射 `wm:documentName` Experience Manager Assets欄位到文檔>名稱Workfront欄位。

1. 按一下 **[!UICONTROL 生成窗體]** 頁籤並拖動 **[!UICONTROL 多行文本]** 的子菜單。 按一下窗體中的元件。 在 **[!UICONTROL 生成窗體]** 頁籤：

   1. 指定 `Document Description` 的 **[!UICONTROL 欄位標籤]** 的子菜單。

   1. 指定 `./jcr:content/metadata/dc:description` 的 **[!UICONTROL 映射到屬性]** 的子菜單。
在Workfront配置映射時，已映射 `dc:description` Experience Manager Assets欄位到文檔>說明Workfront欄位。

1. 按一下 **[!UICONTROL 保存]** 的子菜單。

   >[!VIDEO](https://video.tv.adobe.com/v/344314)

## 將元資料設定應用於影像資料夾 {#apply-metadata-settings-image-folder}

在Experience Manageras a Cloud Service應用程式中配置元資料設定後，將這些設定應用到 [包含從Workfront應用程式發送的映像的資料夾](#send-image-workfront-assets)。

要將元資料設定應用到影像資料夾，請執行以下操作：

1. 導航到 **[!UICONTROL 工具]** > **[!UICONTROL 資產]** > **[!UICONTROL 元資料架構]**。

1. 從可用清單中選擇元資料架構，然後按一下 **[!UICONTROL 應用於資料夾]**。

1. 選擇目標資料夾 [影像是從Adobe Workfront應用程式發送的](#send-image-workfront-assets) 按一下 **[!UICONTROL 應用]**。

您可以導航到Experience Manager Assets中的影像並查看與該影像關聯的元資料。 選擇影像並按一下 **[!UICONTROL 屬性]** 的子菜單。



