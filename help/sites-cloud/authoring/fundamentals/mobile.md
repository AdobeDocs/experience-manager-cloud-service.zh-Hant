---
title: 製作行動裝置的頁面
description: 在製作行動裝置專用的內容時，您可以切換數個模擬器，以檢視使用者所看到的內容
translation-type: tm+mt
source-git-commit: dbd7b8084445b03beff3b5a96b0fa6b5512e10b8

---


# 製作行動裝置的頁面 {#authoring-a-page-for-mobile-devices}

Adobe Experience Manager頁面是以互動式版面為基礎。 自適應版面會自動調整您的內容，以符合目標裝置，毋需針對特定裝置製作內容。

製作行動頁面時，頁面的顯示方式會模擬行動裝置。 在編寫頁面時，您可以在多個模擬器之間切換，以查看使用者在存取頁面時看到的內容。

裝置會根據裝置的功能，分組為類別功能、智慧型和觸控，以呈現頁面。 當使用者存取行動頁面時，AEM會偵測裝置並傳送對應其裝置群組的表示法。

>[!NOTE]
>
>若要根據現有的標準網站建立行動網站，請建立標準網站的即時副本。 請參閱建立適用於不同渠道的即時副本。
>
>AEM開發人員可以建立新的裝置群組。 請參閱建立裝置群組篩選。

<!--
>To create a mobile site based on an existing standard site, create a live copy of the standard site. (See [Creating a Live Copy for Different Channels](/help/sites-administering/msm-livecopy.md).)
>
>AEM developers can create new device groups. (See [Creating Device Group Filters](/help/sites-developing/groupfilters.md).)
-->

請依照下列程式來製作行動頁面：

1. 從全域導覽開啟 **Sites** Console。
1. 編輯內容頁面。
1. 按一下頁面頂端的 **Emulator** 圖示，即可切換至所需的模擬器。

   ![模擬器圖示](/help/sites-cloud/authoring/assets/emulator.png)

1. 將元件從元件瀏覽器或資產瀏覽器拖放至頁面。
1. [根據選取的裝置](/help/sites-cloud/authoring/features/responsive-layout.md) ，修改頁面及其元件的回應式版面配置。

該頁面的外觀類似下列：

![行動裝置範例](/help/sites-cloud/authoring/assets/mobile.png)

>[!NOTE]
>
>當從行動裝置請求作者實例上的頁面時，模擬器被禁用。
