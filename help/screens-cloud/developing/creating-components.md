---
title: 建立元件
description: AEM元件可用來保留、格式化及轉譯可在您的網頁上使用的內容。 請依照本頁面了解製作管道和轉譯元件。
exl-id: a81e812e-29ed-45de-b2d0-1fb0a8c5ce1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 2%

---

# 建立元件 {#creating-components}

AEM元件可用來保留、格式化及轉譯可在您的網頁上使用的內容。

## 製作管道 {#authoring-channels}

頻道是傳遞至一組顯示器的內容的中央物件。 因此，內容作者通常會在編輯器中開啟管道，以新增或修改內容。 由於管道是 ***cq：頁面*** 它會遵循相同的傳統UX模式，在通道上新增和變更元件。

不過，由於管道中的元件通常呈現全螢幕，因此在嘗試編輯單一元件或撰寫新訂單時，製作體驗會受到影響。 因此，通道將仰賴選取器來轉譯元件的不同檢視。 製作環境會利用編輯選取器來啟動自訂通道呈現。

例如， `http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html](http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html`

使用者在編輯時不必將選取器新增至URL。 如果通道具有專用資源類型，則客戶端邏輯正在監聽層交換機事件並添加選擇器 *screens/core/components/channel。*

## 轉譯元件 {#rendering-components}

若要啟用正確的編寫功能，元件必須提供下列兩個呈現：

| **Component** | **轉譯** |
|---|---|
| *my-component/my-component.html* | 生產轉譯 |
| *my-component/edit.html* | 以較小的視圖編輯呈現 |

內建元件利用下列用戶端程式庫類別：

| **元件** | **客戶庫** |
|---|---|
| *cq.screens.components.edit* | CSS和JS，必須在製作期間載入 |
| *cq.screens.components.production* | 頻道執行時必須載入的CSS和JS |
| *cq.screens.components* | 共用CSS和JS |

>[!NOTE]
>
>若要開發自訂元件，請使用***[AEM Screens範例元件範本](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)***。
