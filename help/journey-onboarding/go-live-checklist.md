---
title: 內容上線檢查清單
description: 瞭解使用AEMas a Cloud Service成功上線所需的所有元素
source-git-commit: 4a03e2fe3519fd9e0d8d646526ea6c9cc6637f52
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 6%

---


# 內容上線檢查清單 {#Go-Live-Checklist}

請檢閱此活動清單，以確保您順利成功地上線。

* 執行具有功能和UI測試的端對端生產管道，以確保 **永遠最新** AEM產品體驗。 請參閱下列資源。
   * [AEM 版本更新](/help/implementing/deploying/aem-version-updates.md)
   * [自訂功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [UI 測試](/help/implementing/cloud-manager/ui-testing.md)
* 如果您要從AEM 6.5移轉，您應該將內容移轉至生產環境，並確保中繼上有相關的子集可用於測試。
   * AEM適用的DevOps最佳實務表示程式碼會從開發環境移至生產環境，而內容會從生產環境下移。
* 排程程式碼和內容凍結期間。
   * 另請參閱區段 [移轉的程式碼和內容凍結時間表](#code-content-freeze)
* 執行最終追加內容。
* 驗證Dispatcher設定。
   * 使用本機Dispatcher驗證器，方便您在本機設定、驗證和模擬Dispatcher
      * [設定本機Dispatcher工具](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools.html#prerequisites)
   * 請仔細檢閱虛擬主機組態。
      * 最簡單（也是預設）的解決方案是包含 `ServerAlias *` 虛擬主機檔案中的 `/dispatcher/src/conf.d/available_vhostsfolder`.
         * 如此一來，產品功能測試、Dispatcher快取失效和複製所使用的主機別名就能正常運作。
      * 但是，如果 `ServerAlias *` 不可接受，至少符合下列條件 `ServerAlias` 除了您的自訂網域外，也必須允許輸入專案：
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* 設定CDN、SSL和DNS。
   * 如果您使用自己的CDN，請輸入支援票證以設定適當的路由。
      * 請參閱區段 [客戶CDN指向AEM Managed CDN](/help/implementing/dispatcher/cdn.md#point-to-point-cdn) 詳細資訊，請參閱CDN檔案。
      * 根據您的CDN供應商的檔案設定SSL和DNS。
   * 如果您沒有使用其他CDN，請按照以下檔案管理SSL和DNS：
      * 管理 SSL 憑證
         * [管理 SSL 憑證的簡介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * 管理自訂網域名稱(DNS)
         * 為了確保DNS轉換不會帶來非預期的問題，最好是在您上線並進行一輪UAT測試之前，建立測試子網域以將您的生產執行個體連線到上。 因此，如果您的網域是example.com，您可以建立子網域test.example.com並將其套用至生產環境。 在網域的UAT測試期間，您需要尋找適當的連結重新導向、快取和Dispatcher設定等。
         * [自訂網域名稱簡介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * 請記得驗證DNS記錄的TTL集合。
      * TTL是在要求伺服器更新之前DNS記錄保留在快取中的時間。
      * 如果您的TTL非常高，則傳播DNS記錄的更新將需要更長的時間。
* 執行符合業務需求和目標的效能和安全測試。
   * 在中繼環境中執行測試。  它的大小與生產環境相同。
   * 開發環境與中繼和生產環境的大小不同。
* 請剪下資料，並確定實際上線是在沒有任何新部署或內容更新的情況下執行的。
* 建立Admin Console使用者通知設定檔。 另請參閱 [通知設定檔](/help/journey-onboarding/notification-profiles.md)
* 請考慮設定流量篩選規則來控制網站上不應允許哪些流量。
   * 速率限制流量篩選規則是抵禦DDoS攻擊的有效工具。 流量篩選規則的一種特殊類別（稱為WAF規則）需要單獨的授權。
   * 請參閱檔案以瞭解部分 [建議的入門者規則](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules).

在上線期間，如果您需要重新校準工作，您可以隨時參考清單。