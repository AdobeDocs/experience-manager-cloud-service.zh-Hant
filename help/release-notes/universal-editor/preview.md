---
title: 通用編輯器預覽發行說明
description: 這是通用編輯器預覽版本的發行說明。
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: f3ba70f276ab534e0becea47390fe58bf8a825d2
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 35%

---


# 通用編輯器預覽發行說明 {#preview}

這是通用編輯器&#x200B;**預覽版本**&#x200B;的發行說明。 您目前可以在通用編輯器&#x200B;**預覽環境**&#x200B;中使用這些功能。 這些功能預計於2026年5月7日正式發行。

提供這些&#x200B;**預覽**&#x200B;版本注意事項是為了方便您瞭解即將對通用編輯器進行哪些變更，而且您可以透過[切換至預覽版本來測試這些變更。](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>如需通用編輯器的&#x200B;**最新發行說明**，請參閱[通用編輯器發行說明](/help/release-notes/universal-editor/current.md)文件。

>[!NOTE]
>
>實際發行內容及發行日期可能會有所變動。

## 即將推出的功能 {#upcoming-features}

* 引入了Service Worker來減少通用編輯器UI與後端系統之間的延遲。
* 內容片段（AEM 6.5、OpenAPI和GraphQL）的所有配接卡現在都包含資產選擇器的篩選器，以確保一致性且使用者只能選取允許的資產。
* 現已提供`content:patch`目的。
* 為協助處理無障礙問題，已定義作者流程和地標。

## 其他即將推出的改善專案 {#other-improvements}

* `assignImageDimensionFields`中不必要的型別判斷提示已移除。
* 已修正伺服器端處理`add`作業迭代字串值，將其視為物件而非修補程式的問題。
