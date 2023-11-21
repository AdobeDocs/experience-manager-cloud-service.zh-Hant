---
title: 建立元件
description: AEM元件可用來保留、格式化及轉譯可在網頁上使用的內容。 請依照本頁面的說明了解如何編寫管道和轉譯元件。
exl-id: a81e812e-29ed-45de-b2d0-1fb0a8c5ce1a
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 3%

---

# 建立元件 {#creating-components}

AEM元件可用來保留、格式化及轉譯可在網頁上使用的內容。

## 製作管道 {#authoring-channels}

色版是內容傳送至一組顯示器的中心物件。 因此，內容作者通常會在編輯器中開啟管道，以新增或修改內容。 由於通道是 ***cq：Page*** 它會遵循相同的傳統UX模式，在通道上新增和變更元件。

不過，由於管道中的元件通常會以全熒幕呈現，因此在嘗試編輯單一元件或撰寫新訂單時，編寫體驗會受影響。 因此，管道將依賴選取器來呈現元件的不同檢視。 製作環境會使用編輯選擇器來啟動自訂色版轉譯。

例如 `http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html](http://localhost:4502/editor.html/content/screens/we-retail/channels/idle.edit.html`

使用者在編輯時不必將選擇器新增到URL。 使用者端邏輯正在接聽層切換事件，並在通道具有專用資源型別時新增選取器 *screens/core/components/channel.*

## 演算元件 {#rendering-components}

若要啟用正確製作，元件必須提供下列兩種轉譯：

| **Component** | **轉譯** |
|---|---|
| *my-component/my-component.html* | 生產演算 |
| *my-component/edit.html* | 在較小的檢視中編輯演算 |

內建元件使用下列使用者端程式庫類別：

| **Component** | **客戶庫** |
|---|---|
| *cq.screens.components.edit* | CSS和JS （必須在編寫期間載入） |
| *cq.screens.components.production* | CSS和JS （頻道執行時必須載入） |
| *cq.screens.components* | 共用的CSS和JS |

>[!NOTE]
>
>若要開發自訂元件，請使用***[AEM Screens範例元件範本](https://github.com/Adobe-Marketing-Cloud/aem-screens-component-template)***。
