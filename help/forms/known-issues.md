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

開始使用之前 [!DNL AEM Forms] as a Cloud Service，查看以下已知問題和限制：

## 已知問題 {#known-issues}

* 在另行通知之前，不要添加並運行將自適應表單從發佈實例提交到在AEMAuthor實例上運行的工作流的test。

* 導入使用包含 **[!UICONTROL 保存]** 按鈕 **[!UICONTROL 保存]** 即使從相應模板中刪除該按鈕後，該按鈕仍會繼續顯示在自適應表單中。 刪除 **[!UICONTROL 保存]** 按鈕，然後發佈。 請留意發行說明，瞭解Forms門戶的可用性，並將其另存為草稿功能以還原和使用按鈕。

* 的 **[!UICONTROL 設定變數]** 工作流AEM的步驟不支援類型陣列清單的變數。 可以使用進程步驟設定陣列清單類型的變數。

* 當您從AppleiOS設備提交包含標準HTML上載欄位的自適應表單時，檔案內容不會發送，而在另一端接收0位元組檔案。 此問題間歇性發生，且僅在使用同步提交時發生。 這是 [已知問題](https://feedbackassistant.apple.com/feedback/9117687) 在AppleiOS。

* 當您從AppleiOS設備提交包含標準HTML上載欄位的表單時，有時不會發送檔案內容，在另一端接收0位元組檔案。 這是AppleiOS的一個已知問題。 [FB9117687](https://feedbackassistant.apple.com/feedback/9117687)


## 限制 {#limitations}

* 未提供開箱即用的 XFA 型最適化表單支援。如果您打算使用 XFA 型最適化表單，請聯絡 Adobe 支援並附上使用案例和特定要求的詳細資料。

