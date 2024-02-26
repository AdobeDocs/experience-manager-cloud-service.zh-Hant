---
title: 為行動裝置編寫頁面
description: 為行動裝置製作時，您可以在數個模擬器之間切換，以檢視一般使用者看到的內容
exl-id: fabd4468-3304-402f-9522-342da3bbae94
source-git-commit: a868bf4d4acf4fbae7ccaf55b03319ba0617f9a4
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# 為行動裝置編寫頁面 {#authoring-a-page-for-mobile-devices}

Adobe Experience Manager頁面是以回應式版面為基礎。 [回應式版面](/help/sites-cloud/authoring/page-editor/responsive-layout.md) 會自動調整內容以符合目標裝置，而不需為特定裝置編寫內容。

編寫行動頁面時，頁面會以模擬行動裝置的方式顯示。 編寫頁面時，您可以在多個模擬器之間切換，以檢視一般使用者在存取頁面時看到的內容。

系統會根據裝置轉譯頁面的功能，將裝置分組為類別功能、智慧型和觸控。 當一般使用者存取行動頁面時，AEM會偵測裝置並傳送與其裝置群組相對應的表示。

>[!NOTE]
>
>若要根據現有標準網站建立行動網站，請建立標準網站的即時副本。 另請參閱 [建立即時副本](/help/sites-cloud/administering/msm/creating-live-copies.md).
>
>AEM開發人員可以建立新的裝置群組。 請參閱建立裝置群組篩選器。

<!--
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

請使用下列程式來編寫行動頁面：

1. 從全域導覽開啟 **網站** 主控台。
1. 編輯內容頁面。
1. 按一下「 」以切換至所需的模擬器 **模擬器** 圖示加以存取。

   ![模擬器圖示](/help/sites-cloud/authoring/assets/emulator.png)

1. 從元件瀏覽器或資產瀏覽器將元件拖放至頁面。
1. [修改回應式版面](/help/sites-cloud/authoring/page-editor/responsive-layout.md) 頁面及其元件的URL值。

此頁面外觀類似下列內容：

![行動範例](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>從行動裝置請求製作執行個體上的頁面時，會停用模擬器。
