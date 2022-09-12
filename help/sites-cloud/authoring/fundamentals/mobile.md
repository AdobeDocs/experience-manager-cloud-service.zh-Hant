---
title: 為行動裝置製作頁面
description: 為行動裝置製作內容時，您可以在多個模擬器之間切換，以查看一般使用者所看到的內容
exl-id: fabd4468-3304-402f-9522-342da3bbae94
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 為行動裝置製作頁面 {#authoring-a-page-for-mobile-devices}

Adobe Experience Manager頁面是以回應式版面為基礎。 [回應式版面](/help/sites-cloud/authoring/features/responsive-layout.md) 會自動調整內容以符合目標裝置，而不需要為特定裝置製作內容。

製作行動頁面時，頁面的顯示方式會模擬行動裝置。 編寫頁面時，您可以在多個模擬器之間切換，以查看使用者在存取頁面時所看到的內容。

裝置會根據裝置呈現頁面的功能，分組為類別功能、智慧型和觸控。 當使用者存取行動頁面時，AEM會偵測裝置並傳送與其裝置群組對應的表示法。

>[!NOTE]
>
>若要根據現有標準網站建立行動網站，請建立標準網站的即時副本。 請參閱 [建立即時副本。](/help/sites-cloud/administering/msm/creating-live-copies.md)
>
>AEM開發人員可以建立新裝置群組。 請參閱建立裝置群組篩選器。

<!--
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

請依照下列程式製作行動頁面：

1. 從全局導航開啟 **網站** 控制台。
1. 編輯內容頁面。
1. 按一下 **模擬器** 圖示。

   ![模擬器圖示](/help/sites-cloud/authoring/assets/emulator.png)

1. 將元件從元件瀏覽器或資產瀏覽器拖放至頁面。
1. [修改回應式版面](/help/sites-cloud/authoring/features/responsive-layout.md) 頁面及其元件（根據選取的裝置）。

頁面看起來將類似下列：

![行動範例](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>當從行動裝置要求製作執行個體上的頁面時，模擬器會停用。
