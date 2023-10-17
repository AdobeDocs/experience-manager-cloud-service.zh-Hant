---
title: AEM Formsas a Cloud Service環境的已知問題和限制有哪些？
description: ' [!DNL AEM Forms] as a Cloud Service 環境的已知問題和限制。'
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 7a65aa82792500616f971df52b8ddb6d893ab89d
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 95%

---

# 已知問題和限制 {#known-issues-and-limitations}

開始使用之前[!DNL AEM Forms] as a Cloud Service 之前，請查看以下已知問題和限制：

## 已知問題 {#known-issues}

* 如果測試會將發佈執行個體中的最適化表單提交到在編寫執行個體上執行的 AEM 工作流程，在另行通知之前，請勿新增和執行該測試。

* 當您匯入的最適化表單使用包含&#x200B;**[!UICONTROL 儲存]**&#x200B;按鈕的範本，**[!UICONTROL 儲存]**&#x200B;按鈕即使已從對應的範本中移除，仍會繼續出現在最適化表單中。在發佈之前將&#x200B;**[!UICONTROL 儲存]**&#x200B;按鈕從最適化表單中移除。請密切關注發行說明了解 Forms 入口網站和另存為草稿功能是否可用，以恢復和使用該按鈕。

* AEM 工作流程的&#x200B;**[!UICONTROL 設定變數]**&#x200B;步驟不支援類型陣列清單變數。您可以使用程序步驟來設定類型陣列清單變數。

* 從 Apple iOS 裝置提交包含標準 HTML 上傳欄位的最適化表單時，不會傳送檔案內容且另一端會收到 0 位元組檔案。該問題間歇性發生，且僅在使用同步提交時發生。這是 Apple iOS 的[已知問題](https://feedbackassistant.apple.com/feedback/9117687)。

* 從 Apple iOS 裝置提交包含標準 HTML 上傳欄位的表單時，有時不會傳送檔案內容並在另一端收到 0 位元組檔案。這是 Apple iOS 的已知問題。[FB9117687](https://feedbackassistant.apple.com/feedback/9117687)

* AEM Forms as a Cloud Service 不會產生 XDP 和 JSON 結構描述檔的縮圖。服務會顯示預設圖示來代替縮圖。

  ![表單縮圖已知問題](/help/forms/assets/forms-tumbnail-known-issue.png)

* 當您使用具有可重複元素的結構描述來建立以核心元件為基礎的最適化表單時，從最適化表單編輯器的資料模型樹拖放可重複元素的選項沒有作用。

## 限制 {#limitations}

* 未提供開箱即用的 XFA 型最適化表單支援。如果您打算使用 XFA 型最適化表單，請聯絡 Adobe 支援並附上使用案例和特定要求的詳細資料。

