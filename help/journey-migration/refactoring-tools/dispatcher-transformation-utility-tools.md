---
title: AEM Dispatcher 轉換工具
description: 瞭解如何將AEM Dispatcher上的現有設定轉換為AEM as a Cloud Service Dispatcher上的設定。
exl-id: 2e95ff7b-cc94-477d-99ab-816a58998287
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 28%

---

# AEM Dispatcher 轉換工具 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispconverter"
>title="AEM Dispatcher 轉換工具"
>abstract="Adobe Experience Manager Dispatcher 轉換工具會將現有的 AEM Dispatcher 設定轉換為 AEM as a Cloud Service 設定。"

Adobe Experience Manager Dispatcher 轉換工具會將現有的 AEM Dispatcher 設定轉換為 AEM as a Cloud Service 設定。

## Dispatcher簡介 {#introduction-dispatcher}

Dispatcher是Adobe Experience Manager的快取或負載平衡（或兩者）工具。 使用 AEM 的 Dispatcher 也有助於保護您的 AEM 伺服器不受攻擊。因此，您可以將Dispatcher搭配企業級網頁伺服器使用，以提高AEM執行個體的安全性。

>[!NOTE]
>Dispatcher 最常見的用法是快取來自 **AEM Publish 例項**&#x200B;的回應，以提高您對外發佈網站的回應速度與安全性。

請參閱[Dispatcher概述](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant)，瞭解Dispatcher如何執行快取、傳回檔案和執行負載平衡。

### Apache和Dispatcher設定和測試 {#dispatcher-configurations-cloud}

瞭解如何建構AEM as a Cloud Service Apache和Dispatcher設定，以及如何在部署至雲端環境前，先在本機驗證並執行。

如需詳細資訊，請參閱[雲端中的Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html?lang=zh-Hant)。

## AEM Dispatcher 轉換工具 {#aem-dispatcher-converter}

AEM Dispatcher Converter可將現有的內部部署或Managed Services Dispatcher設定Adobe為與AEM as a Cloud Service相容的Dispatcher設定。

## 使用AEM Dispatcher轉換工具 {#using-dispatcher-converter}

* 透過Adobe Developer CLI ：Adobe建議您透過`aio-cli-plugin-aem-cloud-service-migration`使用AEM Dispatcher Converter (適用於Adobe Developer CLI的AEM as a Cloud Service程式碼重構外掛程式)。

  請參閱&#x200B;**[Git資源： aio-cli-plugin-aem-cloud-service-migration](https://github.com/adobe/aio-cli-plugin-aem-cloud-service-migration#introduction)**，瞭解如何安裝及使用外掛程式。

* 作為獨立公用程式： AEM Dispatcher Converter工具也可以作為獨立公用程式執行。

  請參閱&#x200B;**[Git資源： AEM Cloud Service Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)**，以瞭解此工具的使用和疑難排解資訊。

>[!IMPORTANT]
>AEM Dispatcher Converter是使用NodeJS開發。 Adobe建議您安裝NodeJS 10.0+。
