---
title: 商務多商店設定
description: 了解如何將多個商店檢視從Adobe Commerce對應至AEM。 這可讓專案支援多租用戶和多語言使用案例。
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 4385c9e5-2b25-4f95-952f-72349431cf94,7f6e04a2-89e9-4613-8ea8-9dac1acea30b
source-git-commit: f5e465d90477f1b49e4ff1c5ca9dd47cc5d539bb
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# 商務多商店設定 {#multi-store}

AEM CIF核心元件可用於多個AEM網站結構，且基礎的GraphQL用戶端實作可連線至不同的Adobe Commerce存放區/存放區檢視。 這可讓專案實作複雜的多商店/多網站設定。

詳細說明整合多個Adobe Commerce商店檢視與Adobe Experience Manager Sites選項的視訊逐步說明。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

AEM Live Copy和Language Copy的多網站管理功能與Commerce Integration Framework搭配使用，以全域管理跨地區和地區設定的網站。

建議的設定是使用AEM網站與Adobe Commerce商店檢視之間的1:1關係。

若要連線AEM網站和AEM CIF核心元件以連線至專用商店檢視，請遵循下列步驟：

## 設定 {#configuration}

1. 根據 [Adobe Commerce網站、商店和檢視](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. 請確定AEM與Adobe Commerce之間的連線正常運作。

3. 依照下列步驟建立CIFCloud Service設定的子設定：

   * 在AEM中，轉至「工具」 — >「一般」 — > [配置瀏覽器](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * 選取您建立的基礎設定
   * 使用上述第2點所述步驟建立新配置

   此新配置將建立為基本配置的子配置。 您現在可以前往「工具」 — >「一般」 — >「組態瀏覽器」，並建立組態設定。

   >[!TIP]
   >
   > 可使用ID或UID來定址商務目錄。 Adobe Commerce 2.4.2導入了UID。只有在您的商務後端支援2.4.2版或更新版本的GraphQL架構時，才啟用此功能。

4. 將子配置指派給AEM站點

   * 前往AEM Sites主控台
   * 導覽至網站結構的地區或語言根目錄，例如/content/venia/us _或_ Venia範例頁面的/content/venia/us/en
   * 選取頁面並開啟頁面屬性
   * 選擇「高級」頁簽
   * 在 `Configuration` 區段選取您在步驟3建立的設定

## 其他資源

* [Adobe Commerce網站、商店和檢視](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF核心元件 — 多商店/網站設定](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [使用多網站管理員](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [重複使用內容：多網站管理員和即時副本](/help/sites-cloud/administering/msm/overview.md)
