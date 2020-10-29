---
title: 多商店設定
description: 瞭解如何將Magento中的多個商店檢視對應至AEM。 這可讓專案支援多租用戶和多語言使用案例。
sub-product: 商務
version: cloud-service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
translation-type: tm+mt
source-git-commit: 4862a09b3a0ce2f7506f4fff10639c51792db1b7
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 1%

---


# 多商店設定 {#multi-store}

AEM CIF核心元件可用於多個AEM網站結構，而基礎的GraphQL用戶端實作可連接至不同的Magento儲存／儲存檢視。 這可讓專案建置複雜的多商店／多網站設定。

視訊逐步說明將多個Magento商店檢視與Adobe Experience Manager Sites整合的選項。

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

「即時副本」和「語言副本」的AEM多網站管理功能與「商務整合架構」搭配使用，以全面管理各地區和地區的網站。

建議的設定是使用AEM網站和Magento商店檢視之間的1:1關係。

若要將AEM網站和AEM CIF核心元件連接至專用的商店檢視，請遵循下列步驟：

## 設定 {#configuration}

1. 根據 [Magento Websites、Stores &amp; Views中描述的模式，設定多個商店和商店檢視](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. 請確定AEM和Magento之間的連線正在運作。

3. 按照以下步驟建立CIF雲服務配置的子配置：

   * 在AEM中，請至「工具->一般->設定瀏 [覽器」](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * 選擇您建立的基本配置
   * 使用上述第2點所述的步驟建立新組態

   此新配置將建立為基本配置的子配置。 您現在可以前往「工具」->「一般」->「設定瀏覽器」並建立設定設定。

4. 將子項設定指派給AEM網站

   * 前往AEM Sites主控台
   * 導覽至網站結構的地區或語言根目錄，例如/content/venia/us _或_ /content/venia/us/tw/en for the Venia sample page
   * 選擇頁面並開啟頁面屬性
   * 選擇「高級」頁籤
   * 在節 `Configuration` 中，選擇在步驟中建立的配置

## 其他資源

* [Magento網站、商店和檢視](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [AEM CIF核心元件——多商店／網站組態](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [使用多網站管理員](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [重複使用內容：多網站管理員和即時副本](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/msm.html)
