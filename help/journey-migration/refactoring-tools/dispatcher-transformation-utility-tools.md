---
title: AEM Dispatcher 轉換工具
description: AEM Dispatcher 轉換工具
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
source-git-commit: a9aa82c8258e6a5f43680069c65518093c0baf8d
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 24%

---

# AEM Dispatcher 轉換工具 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher 轉換工具"
>abstract="Adobe Experience Manager Dispatcher Converter會將AEM Dispatcher上的現有設定轉換為AEMas a Cloud ServiceDispatcher上的設定。"

Adobe Experience Manager Dispatcher Converter會將AEM Dispatcher上的現有設定轉換為AEMas a Cloud ServiceDispatcher上的設定。

## Dispatcher 簡介 {#introduction-dispatcher}

Dispatcher是Adobe Experience Manager的快取、負載平衡或兩者兼而有之的工具。 使用 AEM 的 Dispatcher 也有助於保護您的 AEM 伺服器不受攻擊。因此，您可以將Dispatcher搭配企業級網頁伺服器使用，以提高AEM執行個體的安全性。

>[!NOTE]
>Dispatcher 最常見的用法是快取來自 **AEM Publish 例項**&#x200B;的回應，以提高您對外發佈網站的回應速度與安全性。

請參閱 [Dispatcher總覽](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant) 以瞭解Dispatcher如何執行快取、傳回檔案和執行負載平衡。

### Apache 和 Dispatcher 設定和測試 {#dispatcher-configurations-cloud}

瞭解如何建構AEMas a Cloud Service的Apache和Dispatcher設定，以及如何在部署至雲端環境之前在本機驗證和執行它。

另請參閱 [雲端中的Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html) 以取得詳細資訊。

## AEM Dispatcher 轉換工具 {#aem-dispatcher-converter}

AEM Dispatcher Converter可將現有的內部部署或Adobe Managed Services Dispatcher設定重構成與AEMas a Cloud Service相容的Dispatcher設定。

## 使用 AEM Dispatcher 轉換工具 {#using-dispatcher-converter}

* 透過Adobe Developer CLI ：Adobe建議您透過以下方式使用AEM Dispatcher Converter： `aio-cli-plugin-aem-cloud-service-migration` (Adobe Developer CLI的AEMas a Cloud Service程式碼重構外掛程式)。

  另請參閱 **[Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)** 以便您瞭解如何安裝及使用外掛程式。

* 作為獨立公用程式： AEM Dispatcher Converter工具也可以作為獨立公用程式執行。

  另請參閱 **[Git資源： AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)** 以便您瞭解此工具的使用和疑難排解。

>[!IMPORTANT]
>AEM Dispatcher Converter是使用NodeJS開發。 Adobe建議您安裝NodeJS 10.0+。
