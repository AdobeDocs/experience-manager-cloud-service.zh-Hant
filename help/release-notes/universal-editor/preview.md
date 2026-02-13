---
title: 通用編輯器預覽發行說明
description: 這是通用編輯器預覽版本的發行說明。
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: 374c8045043f67f06d4ae68aef499bb594f1c08c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 29%

---

# 通用編輯器預覽發行說明 {#preview}

這是通用編輯器&#x200B;**預覽版本**&#x200B;的發行說明。您目前可以在通用編輯器&#x200B;**預覽環境**&#x200B;中使用這些功能。這些功能預計於2026年2月19日正式發行。

提供這些&#x200B;**預覽**&#x200B;版本注意事項是為了方便您瞭解即將對通用編輯器進行哪些變更，而且您可以透過[切換至預覽版本來測試這些變更。](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>如需通用編輯器的&#x200B;**最新發行說明**，請參閱[通用編輯器發行說明](/help/release-notes/universal-editor/current.md)文件。

>[!NOTE]
>
>實際發行內容及發行日期可能會有所變動。

## 即將推出的新功能 {#what-is-new}

* 已改善RTE。
   * 現在支援在內容RTE中隱藏工具列專案。
   * 現在支援在表格內以段落繞排文字。
   * 現在會保留不支援的RTE標籤。
   * RTE邏輯現在由個別檔案提供。
   * 現在可以使用RTE建立或編輯表格。
* 如果未設定標籤，則現在會使用元件定義中的元件標題。
* `setEditorMode`現在可透過擴充功能使用。

## 即將推出的改善功能 {#other-improvements}

* 已修正頁面之間的複製並貼上功能。
* `universal-editor-extensibility`已移至`universal-editor`。
* 對擴充功能端點的要求數量已減少。
* RemoteApp解除安裝已從三個減少至一個。
* RTE端點現在可供就地編輯器使用。
* 編輯巢狀欄位不再導致從這些結構覆寫對等專案。
* 強制RTE欄位無法再儲存為空白。
* 在格式化後新增連結時，就地格式不再不當套用。
