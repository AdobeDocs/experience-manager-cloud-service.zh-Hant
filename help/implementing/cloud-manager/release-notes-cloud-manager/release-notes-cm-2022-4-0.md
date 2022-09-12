---
title: Adobe Experience Manager as a Cloud Service中Cloud Manager 2022.4.0發行說明
description: 以下是AEM as a Cloud Service中Cloud Manager 2022.4.0的發行說明。
feature: Release Information
exl-id: e7ff623b-aeca-40a6-bf48-98af270a4117
source-git-commit: 458d63c27bb2ab4d09237aa3ecb96c0f6d5e67ed
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud Service中Cloud Manager 2022.4.0發行說明 {#release-notes}

本頁記錄AEM as a Cloud Service中Cloud Manager 2022.4.0的發行說明。

>[!NOTE]
>
>請參閱 [本頁](/help/release-notes/release-notes-cloud/release-notes-current.md) Adobe Experience Manager as a Cloud Service的最新發行說明。

## 發行日期 {#release-date}

AEMas a Cloud Service中Cloud Manager 2022.4.0版的發行日期為2022年4月7日。 下一版預計於2022年5月5日發行。

## 新增功能 {#what-is-new}

* 管道建置步驟的持續時間和成功率已實作改善，並將在4月整個月逐步推出給所有客戶。
* 您現在可以在新增和編輯管道精靈的輸入欄位中輸入名稱的前幾個字元，並從兩者的建議相符項目中選取，輕鬆找到Git分支 [生產](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 和 [非生產](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 管道。
* 4月版發佈後不久，在環境建立期間定義雲端地區時，印度即可供選取。
* 此 **管道** 頁面現在具有分頁功能，可改善具有大量管道之程式的可用性。
   * 表格中會顯示每頁50列。
* 版本 [AEM專案原型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) Cloud Manager使用的已更新至36版。
* OracleJDK現在是AEM應用程式開發與運作的預設JDK。 即使在Maven工具鏈中明確選取了替代選項，Cloud Manager建置程式仍會自動切換為使用OracleJDK。
   * 若要進一步了解如何切換至OracleJDK，請參閱 [建置環境檔案。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#using-java-support)
   * 請參閱 [Adobe Experience Manager的Java支援政策常見問題集](https://experienceleague.adobe.com/docs/experience-manager-65/assets/Java_Policy_for_Adobe_Experience_Manager.pdf) 來解決有關此變更的常見問題。
* 現在，在驗證步驟期間偵測到舊版AEM，可讓管道執行更快失敗。 使用者在UI中會收到訊息，以引導他們。

## 錯誤修正 {#bug-fixes}

* 在UI測試步驟中建立的記錄檔現在可透過UI下載。
* Web層配置管道現在只能重複使用Web層配置執行中的包。
* UI中的訊息更清楚說明如何在過時的環境中更新AEM。
