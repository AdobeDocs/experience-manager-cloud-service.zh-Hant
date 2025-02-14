---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.2.0 的發行說明
description: 了解 AEM as a Cloud Service 中 Cloud Manager 2025.2.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: aaef376b733c10643e44205e55a0921c22008990
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 15%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.2.0 的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.2.0 的發行資訊。


另請參閱Adobe Experience Manager as a Cloud Service ](/help/release-notes/release-notes-cloud/release-notes-current.md)的[最新發行說明。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.2.0發行日期是2025年2月13日星期四。

下一個預計發行日期為2025年3月13日星期四。

## 新增功能 {#what-is-new}

* **程式碼品質規則的更新**

  從2025年2月13日星期四開始，Cloud Manager程式碼品質步驟現在使用SonarQube 9.9.5.90363。

  更新的規則適用於AEM as a Cloud Service上的Cloud Manager （位於[此連結](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules)），可決定Cloud Manager管道的安全性分數和程式碼品質。

* SonarQube 9.9現在是所有客戶的預設程式碼品質掃描引擎。

* **Java 17和Java 21組建支援**

  客戶現在可以使用Java 17或Java 21進行建置，以獲得效能增強功能和新語言功能。 若要了解設定步驟 (包括更新 Maven 專案和資料庫版本)，請參閱「[建置環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)」。當建置版本設定為 Java 17 或 Java 21 時，部署的執行階段為 Java 21。

* **適用於Edge Delivery Services的SLA正常運作時間報告功能**

  高可用性99.99%的連續運作時間報告現在可用於符合資格的Edge Delivery Services計畫。 若要啟用此功能，客戶必須成功上線其Edge Delivery Services網站，並在Cloud Manager中套用其99.99%的Service level agreement (SLA)。

  另請參閱[SLA](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md#sla)。

* **改善Edge Delivery Services的使用者邀請體驗**

  邀請使用者加入與Edge Delivery Services相關聯的內容存放庫的體驗已有所改善。<!-- CMGR-65331 -->

* **在發佈執行個體上自動建立管理員設定檔**

  之前，Cloud Manager允許在發佈執行個體上手動建立管理員設定檔，但預設不支援自動建立。 透過此更新，現在可在發佈執行個體上自動建立管理員設定檔，從而提高可用性並縮短客戶的設定時間。

  如需詳細資訊，請參閱[自訂許可權](/help/implementing/cloud-manager/custom-permissions.md)。

  ![管道活動篩選](/help/implementing/cloud-manager/release-notes/assets/product-profiles.png)

* **轉換至Cloud Service環境的OAuth**

  新的Cloud Service環境現在會針對Adobe Developer Console整合專案使用OAuth型服務對服務驗證，而非先前使用的JWT驗證方法。 JWT驗證已過時，並計畫於2025年6月終止服務。

* **支援EC （橢圓曲線）私密金鑰(secp384r1)**

  Cloud Manager現在支援`secp384r1`橢圓曲線(EC)私密金鑰，提供客戶管理的OV/EV SSL憑證的改良安全性與合規性。
如需詳細資訊，請參閱[客戶管理的OV/EV SSL憑證需求](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)。<!-- CMGR-63636 -->

* **專門的測試環境**

  具有增強型資源的新開發環境將於2025年2月27日開始提供給早期採用者。


<!--
## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->


## 錯誤修正

* **(UI)修正Cloud Manager中無法設定網域CDN的問題。**
客戶嘗試在Cloud Manager中新增CDN設定時，從下拉式選單中選取網域時遭遇熒幕錯誤。 這個使用者介面的錯誤使得生產環境中的網域對應無法進行，進而封鎖了設定程式。

  此外，儘管已從使用者介面中移除某些網域，這些網域在後端仍無法存取。 此問題會導致與現有CDN設定衝突。

  透過此修正，您現在可以從下拉式清單中成功選取網域，而不會發生錯誤。 已解決阻止重新配置網域的後端不一致。 最後，改善的驗證現在可確保衝突網域在重新新增之前已正確移除。<!-- CMGR-64888 -->
* **（後端）修正導致SSL到期通知多次傳送的問題。**
已識別出以下錯誤：SSL到期通知排程器（設計為在午夜每日執行一次）每天錯誤地觸發兩次(在午夜觸發一次，然後在午夜12:30再次觸發。 此問題導致傳送多個有關過期SSL憑證的重複通知。

  通知排程器現在每天只能正確執行一次。 而且，您不會再收到重複的SSL到期通知。<!-- CMGR-64748 -->




<!-- ## Known issues {#known-issues} -->
