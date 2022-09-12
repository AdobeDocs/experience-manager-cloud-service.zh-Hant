---
title: 已知問題和限制
description: 已知問題和限制  [!DNL AEM Forms] as a Cloud Service環境
contentOwner: khsingh
role: User, Developer
level: Intermediate
topic: Administration
exl-id: 871f294d-f251-4966-a021-39df65b613f0
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 12%

---

# 已知問題和限制 {#known-issues-and-limitations}

開始使用之前 [!DNL AEM Forms] as a Cloud Service，請檢閱下列已知問題和限制：

## 已知問題 {#known-issues}

* 在進一步通知前，請勿新增並執行測試，該測試會從發佈例項提交至在製作例項上執行的AEM工作流程。

* 匯入使用包含 **[!UICONTROL 儲存]** 按鈕 **[!UICONTROL 儲存]** 按鈕從對應範本中移除後，仍會繼續顯示在適用性表單中。 移除 **[!UICONTROL 儲存]** 按鈕，再發佈。 請留意發行說明，了解Forms Portal的可用性，並將「另存為」功能儲存為草稿，以還原及使用按鈕。

* 此 **[!UICONTROL 設定變數]** AEM工作流程的步驟不支援陣列清單類型的變數。 您可以使用處理步驟來設定陣列清單類型的變數。

* 當您從Apple iOS裝置提交包含標準HTML上傳欄位的最適化表單時，不會傳送檔案內容，且另一端會收到0位元組檔案。 此問題間歇性發生，且僅在使用同步提交時發生。 這是 [已知問題](https://feedbackassistant.apple.com/feedback/9117687) 在AppleiOS。

* 當您從Apple iOS裝置提交包含標準HTML上傳欄位的表單時，有時不會傳送檔案內容，且另一端會收到0位元組檔案。 這是Apple iOS的已知問題。 [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)


## 限制 {#limitations}

* 未提供開箱即用的 XFA 型最適化表單支援。如果您打算使用 XFA 型最適化表單，請聯絡 Adobe 支援並附上使用案例和特定要求的詳細資料。

