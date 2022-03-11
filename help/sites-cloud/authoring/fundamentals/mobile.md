---
title: 為移動設備創作頁面
description: 在為移動版創作時，您可以在多個模擬器之間切換，以查看最終用戶看到的內容
exl-id: fabd4468-3304-402f-9522-342da3bbae94
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 為移動設備創作頁面 {#authoring-a-page-for-mobile-devices}

Adobe Experience Manager頁面基於響應佈局。 [響應式佈局](/help/sites-cloud/authoring/features/responsive-layout.md) 自動調整內容以適應目標設備，從而消除了為特定設備編寫內容的需要。

當創作移動頁面時，以模擬移動設備的方式顯示頁面。 創作頁面時，可以在多個模擬器之間切換以查看最終用戶在訪問頁面時看到的內容。

根據設備的功能將設備分組到類別特徵、智慧和觸摸以呈現頁面。 當終端用戶訪問移動頁面時，AEM檢測設備併發送對應於其設備組的表示。

>[!NOTE]
>
>要基於現有標準站點建立移動站點，請建立標準站點的即時副本。 請參閱 [建立即時副本。](/help/sites-cloud/administering/msm/creating-live-copies.md)
>
>開AEM發人員可以建立新設備組。 請參閱建立設備組篩選器。

<!--
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

請按下列步驟編寫移動頁面：

1. 從全局導航開啟 **站點** 控制台。
1. 編輯內容頁面。
1. 通過按一下 **模擬器** 表徵圖

   ![模擬器表徵圖](/help/sites-cloud/authoring/assets/emulator.png)

1. 將元件從元件瀏覽器或資產瀏覽器拖放到頁面。
1. [修改響應佈局](/help/sites-cloud/authoring/features/responsive-layout.md) 基於所選設備的頁面及其元件。

該頁面將類似於以下內容：

![移動示例](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>當從移動設備請求作者實例上的頁面時，模擬器被禁用。
