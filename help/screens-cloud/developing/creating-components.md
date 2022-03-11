---
title: 建立元件
description: 組AEM件用於保存、格式化和呈現網頁上提供的內容。 請按照此頁瞭解創作渠道和渲染元件。
exl-id: a81e812e-29ed-45de-b2d0-1fb0a8c5ce1a
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 2%

---

# 建立元件 {#creating-components}

組AEM件用於保存、格式化和呈現網頁上提供的內容。

## 創作渠道 {#authoring-channels}

該頻道是傳遞到一組顯示器的內容的中心對象。 因此，內容作者通常會在編輯器中開啟一個頻道來添加或修改內容。 因為頻道是 ***cq：頁*** 它將遵循相同的傳統UX模式在通道上添加和更改元件。

但是，由於通道中的元件通常呈現全屏，因此在嘗試編輯單個元件或編寫新訂單時，創作體驗會受到影響。 因此，通道將依靠選擇器來呈現元件的不同視圖。 創作環境將利用編輯選擇器來激活自定義通道呈現。

例如， `http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html](http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html`

用戶在編輯時不必將選擇器添加到URL。 客戶端邏輯正在偵聽層交換機事件，並且如果通道具有專用資源類型，則添加選擇器 *螢幕/核心/元件/通道。*

## 渲染元件 {#rendering-components}

要啟用正確的創作，元件需要提供以下兩種渲染：

| **元件** | **轉譯** |
|---|---|
| *my-component/my-component.html* | 生產渲染 |
| *my-component/edit.html* | 在較小視圖中編輯渲染 |

內置元件利用以下客戶端庫類別：

| **元件** | **客戶庫** |
|---|---|
| *cq.screens.components.edit* | CSS和JS，在創作過程中必須載入 |
| *cq.screens.components.production* | 在通道運行時必須載入的CSS和JS |
| *cq.screens.components* | 共用CSS和JS |

>[!NOTE]
>
>要開發自定義元件，請使用***[AEM Screens樣本元件模板](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)***。
