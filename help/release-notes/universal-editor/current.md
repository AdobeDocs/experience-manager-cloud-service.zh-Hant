---
title: 通用編輯器 2026.03.19 發行說明
description: 此為通用編輯器 2026.03.19 版本的發行說明。
feature: Release Information
role: Admin
exl-id: d16ed78d-d5a3-45bf-a415-5951e60b53f9
source-git-commit: 8d9d162ec5bba99afb1ae86252a49a9880be4e68
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 42%

---


# 通用編輯器 2026.03.19 發行說明 {#release-notes}

以下是通用編輯器 2026 年 3 月 19 日版本的發行說明。

>[!TIP]
>
>如果您想在發行之前測試&#x200B;**即將推出的**&#x200B;通用編輯器功能，請參閱[通用編輯器預覽發行說明。](/help/release-notes/universal-editor/preview.md)

>[!TIP]
>
>如需 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[此頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 新增功能 {#what-is-new}

* 現在當導覽回[主畫面時，屬性中的專案會摺疊。](/help/sites-cloud/authoring/universal-editor/navigation.md#home-button)
* [資產選擇器](/help/implementing/universal-editor/configure-assets-selector.md)現在支援[篩選器定義。](/help/implementing/universal-editor/filtering.md)
* 如果選取的專案沒有可用的動作，[內容功能表](/help/sites-cloud/authoring/universal-editor/authoring.md#context-menu)就不會再顯示>形箭號來存取動作。

## 其他改善功能 {#other-improvements}

* 如果有模型/篩選器/元件定義，則在編輯器中，從某個應用程式切換到另一個應用程式時，將會重新擷取該定義。
* 使用DA做為後端時，移除影像不會再留下空白的影像標籤。
* 現在當使用DA做為後端時，區塊中的類別可正確處理。
* Open API現在會將遠端資產正確儲存為物件。

## 重大變更 {#breaking-change}

* 所有擴充功能都應更新為`@adobe/uix-guest` >= `1.1.7`以提高穩定性。
