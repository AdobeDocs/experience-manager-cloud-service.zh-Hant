---
title: Universal Editor 2026.05.07發行說明
description: 這些是2026.05.07版通用編輯器的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 4f66cd6048d7a78bea33c0f9c21017983b9032d5
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 12%

---


# Universal Editor 2026.05.07發行說明 {#release-notes}

以下是2026年5月7日發行的Universal Editor的發行說明。

>[!TIP]
>
>如果您想在發行之前測試&#x200B;**即將推出的**&#x200B;通用編輯器功能，請參閱[通用編輯器預覽發行說明。](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>如需Adobe Experience Manager as a Cloud Service目前的發行說明，請參閱[此頁面。](/help/release-notes/release-notes-cloud/release-notes-current.md)

## 新增功能 {#what-is-new}

* 您現在可以在編輯器中[拖放元件，以移動它們。](/help/sites-cloud/authoring/universal-editor/authoring.md#drag-and-drop-move)
* 引入了Service Worker來減少通用編輯器UI與後端系統之間的延遲。
* 內容片段（AEM 6.5、OpenAPI和GraphQL）的所有配接卡現在都包含資產選擇器的篩選器，以確保一致性且使用者只能選取允許的資產。
* 現已提供`content:patch`目的。
* 為協助處理無障礙問題，已定義作者流程和地標。

## 其他即將推出的改善專案 {#other-improvements}

* `assignImageDimensionFields`中不必要的型別判斷提示已移除。
* 已修正伺服器端處理`add`作業迭代字串值，將其視為物件而非修補程式的問題。
