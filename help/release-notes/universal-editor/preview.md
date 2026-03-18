---
title: 通用編輯器預覽發行說明
description: 這是通用編輯器預覽版本的發行說明。
feature: Release Information
role: Admin
exl-id: e8d031aa-4676-4e45-977b-e5dffcc404c4
source-git-commit: bbf371dbf8102611345f2d289a3eaba56ee1d87c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 33%

---


# 通用編輯器預覽發行說明 {#preview}

這是通用編輯器&#x200B;**預覽版本**&#x200B;的發行說明。您目前可以在通用編輯器&#x200B;**預覽環境**&#x200B;中使用這些功能。這些功能預計於2026年3月12日正式發行。

提供這些&#x200B;**預覽**&#x200B;版本注意事項是為了方便您瞭解即將對通用編輯器進行哪些變更，而且您可以透過[切換至預覽版本來測試這些變更。](/help/sites-cloud/authoring/universal-editor/navigation.md#user-properties)

>[!TIP]
>
>如需通用編輯器的&#x200B;**最新發行說明**，請參閱[通用編輯器發行說明](/help/release-notes/universal-editor/current.md)文件。

>[!NOTE]
>
>實際發行內容及發行日期可能會有所變動。

## 即將推出的功能 {#upcoming-features}

* 現在可以在主畫面上收合右側邊欄中的專案。
* 資產選擇器現在支援篩選器定義。
* 如果選取的專案沒有可用的動作，內容功能表就不會再顯示>形箭號來存取動作。

## 即將推出的改善功能 {#upcoming-improvements}

* 如果有模型/篩選器/元件定義，則在編輯器中，從某個應用程式切換到另一個應用程式時，將會重新擷取該定義。
* 使用DA做為後端時，移除影像不會再留下空白的影像標籤。
* 現在當使用DA做為後端時，區塊中的類別可正確處理。
* Open API現在會將遠端資產正確儲存為物件。

## 即將到來的重大變更 {#breaking-change}

* 所有擴充功能都應更新為`@adobe/uix-guest` >= `1.1.7`以提高穩定性。
