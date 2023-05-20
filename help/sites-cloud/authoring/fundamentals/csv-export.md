---
title: 匯出為 CSV
description: 將有關頁面的資訊導出到本地系統上的CSV檔案
exl-id: 818e927e-40b2-4ccb-bfb3-88284ad49829
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 42%

---

# 匯出為 CSV {#export-to-csv}

**建立CSV報告** 允許您將有關頁面的資訊導出到本地系統上的CSV檔案。

* 已下載的檔案稱為 `export.csv`
* 內容取決於您選擇的屬性。
* 可以定義路徑和導出深度。

>[!NOTE]
>
>使用瀏覽器的下載功能和預設目標。

「建 **立CSV匯出** 」精靈可讓您選擇：

* 要匯出的屬性
   * 中繼資料
      * 名稱
      * 修改時間
      * 已發佈
      * 範本
      * 工作流程
   * 轉換
      * 已翻譯
   * 分析
      * 頁面檢視
      * 不重複訪客
      * 頁面逗留時間
* 深度
   * 父路徑
   * 僅導向子項
   * 其他層級的子項
   * 層級

結果 `export.csv` 可以在Excel或任何其他相容應用程式中開啟檔案。

要建立CSV導出：

1. 開啟 **Sites** Console，視需要導覽至所需位置。
   * 瀏覽Sites **控制台時**  (在「清單」檢視中)，可使用「建立 **CSV報表** 」選項
   * 它是 **建立** 下拉菜單：

      ![建立CSV選項](/help/sites-cloud/authoring/assets/csv-create.png)

1. 從工具列中，依序選 **取「建立****CSV報表** 」以開啟精靈：

   ![CSV導出選項](/help/sites-cloud/authoring/assets/csv-options.png)

1. 選擇要導出的必需屬性。
1. 選擇 **建立**。
   ![在Excel中導出結果CSV](/help/sites-cloud/authoring/assets/csv-example.png)
