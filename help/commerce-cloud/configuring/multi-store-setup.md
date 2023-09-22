---
title: Commerce多商店設定
description: 瞭解如何從Adobe Commerce將多個商店檢視對應至Adobe Experience Manager。 如此一來，專案便可支援多租使用者和多語言使用案例。
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 4385c9e5-2b25-4f95-952f-72349431cf94
source-git-commit: 97a6a7865f696f4d61a1fb4e25619caac7b68b51
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 2%

---

# Commerce多商店設定 {#multi-store}

Adobe Experience Manager (AEM) CIF核心元件可用於多個AEM網站結構，而基礎的GraphQL使用者端實作可連線至不同的Adobe Commerce商店/商店檢視。 如此一來，專案便可實作複雜的多商店/多網站設定。

逐步解說影片，詳述將多個Adobe Commerce商店檢視與Adobe Experience Manager Sites整合的選項。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

Live Copy和Language Copy的AEM多網站管理功能可與Commerce Integration Framework搭配使用，以便全域管理跨區域和區域設定的網站。

建議的設定是使用AEM網站與Adobe Commerce商店檢視之間的1:1關係。

若要將AEM網站和AEM CIF核心元件連線至專用的存放區檢視，請執行以下操作：

## 設定 {#configuration}

1. 根據中所述的模式設定多個商店和商店檢視 [Adobe Commerce網站、商店和檢視](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)

2. 請確定AEM與Adobe Commerce之間的連線正常運作。

3. 按照以下步驟建立CIFCloud Service設定的子設定：

   * 在AEM中，前往「工具」 — >「一般」 — > [設定瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * 選取您建立的基本組態
   * 使用上述第2點所述的步驟建立設定

   此新組態會建立為基底組態的子組態。 您現在可以前往「工具」 — >「一般」 — >「組態瀏覽器」並建立組態設定。

   >[!TIP]
   >
   > 商業目錄可使用ID或UID來處理。 Adobe Commerce 2.4.2匯入了UID。只有在您的Commerce後端支援2.4.2版或更新版本的GraphQL結構描述時，才會啟用此功能。

4. 將子組態指派至AEM站台

   * 前往AEM Sites主控台
   * 導覽至您網站結構的區域或語言根目錄。 例如， `/content/venia/us _or_ /content/venia/us/en` 針對Venia範例頁面
   * 選取頁面並開啟頁面屬性
   * 選取「進階」標籤
   * 在 `Configuration` 區段，選取您在步驟3建立的組態

## 其他資源

* [Adobe Commerce網站、商店和檢視](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)
* [AEM CIF核心元件 — 多商店/網站設定](https://github.com/adobe/aem-core-cif-components#multi-store--site-configuration)
* [使用多站點管理員](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [重複使用內容：多網站管理員和 Live Copy](/help/sites-cloud/administering/msm/overview.md)
