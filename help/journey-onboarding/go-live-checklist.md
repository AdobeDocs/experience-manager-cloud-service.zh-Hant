---
title: 上線檢查清單
description: 瞭解成功使用AEM as a Cloud Service上線所需的所有元素。
exl-id: b424a9db-0f3b-4a8d-be84-365d68df46ca
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 4a369104ea8394989149541ee1a7b956383c8f12
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 56%

---

# 上線檢查清單 {#Go-Live-Checklist}

查看此活動清單，確保您的上線過程順利且成功。

* 透過功能性與 UI 測試來執行端對端生產管道，確保擁有&#x200B;**永遠最新**&#x200B;的 AEM 產品體驗。請參閱下列資源。
   * [AEM 版本更新](/help/implementing/deploying/aem-version-updates.md)
   * [自訂功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)
   * [UI 測試](/help/implementing/cloud-manager/ui-testing.md)
* 如果您是從 AEM 6.5 移轉，應將內容移轉到生產環境，並確保相關子集可用於測試的預備作業。
   * AEM 的 DevOps 最佳實務意味著程式碼要從開發環境向上移動到生產環境，內容則從生產環境向下移動。
* 安排程式碼與內容凍結期間。
   * 另請參閱「[移轉作業的程式碼和內容凍結時間表](#code-content-freeze)」小節
* 追加最後的內容。
* 驗證Dispatcher設定。
   * 使用本機Dispatcher驗證器，協助您在本機設定、驗證和模擬Dispatcher
      * [設定本機Dispatcher工具](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/dispatcher-tools#prerequisites)。
   * 仔細檢查虛擬主機設定。
      * 最簡單（且預設）的解決方案是將`ServerAlias *`包含在`/dispatcher/src/conf.d/available_vhostsfolder`的虛擬主機檔案中。 如此一來，產品功能測試、Dispatcher快取失效和複製所使用的主機別名即可正常運作。
      * 但是，如果無法接受`ServerAlias *`，則除了您的自訂網域之外，至少必須允許下列`ServerAlias`個專案：
         * `localhost`
         * `*.local`
         * `publish*.adobeaemcloud.net`
         * `publish*.adobeaemcloud.com`
* 設定內容傳遞網路、SSL 和 DNS。
   * 如果您使用自己的內容傳遞網路，請輸入支援服務單以設定適當的傳送路徑。
      * 如需詳細資訊，請參閱內容傳遞網路文件中的「[客戶內容傳遞網路指向 AEM 管理的內容傳遞網路](/help/implementing/dispatcher/cdn.md#point-to-point-cdn)」小節。
      * 根據 CDN 供應商的文件設定 SSL 和 DNS。
   * 如果您未使用額外的 CDN，請依照下列文件管理 SSL 和 DNS：
      * 管理 SSL 憑證
         * [管理SSL憑證的簡介](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
         * [管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
      * 管理自訂網域名稱 (DNS)
         * 請確定DNS切換不會造成非預期的問題。 在您上線並進行一輪UAT測試之前，請建立測試子網域以將您的生產執行個體連線到上。 因此，如果您的網域是example.com，您可以建立子網域test.example.com並將其套用至生產環境。 在網域的UAT測試期間，尋找適當的連結重新導向、快取和Dispatcher設定等內容。
         * [自訂網域名稱簡介](/help/implementing/cloud-manager/custom-domain-names/introduction.md)
         * [新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)
         * [管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)
   * 請記得驗證您的 DNS 記錄的 TTL 集合。
      * TTL 是 DNS 記錄向伺服器請求更新之前保留在快取中的時間量。
      * 如果您的TTL非常高，則需要較長的時間才能傳播DNS記錄的更新。
* 執行符合您的業務要求和目標的效能與安全測試。
   * 在中繼環境中執行測試。  它的規模與生產環境相同。
   * 開發環境的規模與中繼和生產環境不同。
* 切換並確保在沒有任何新部署或內容更新的情況下執行實際的上線。
* 建立Admin Console使用者通知設定檔。 請參閱[通知設定檔](/help/journey-onboarding/notification-profiles.md)
* 考慮設定流量篩選規則來控制您的網站上不應允許哪些流量。
   * 速率限制流量篩選規則是抵禦DDoS攻擊的有效工具。 流量篩選規則的一種特殊類別，稱為WAF （Web應用程式防火牆）規則，需要單獨的授權。
   * 請參閱文件了解一些[建議入門規則](/help/security/traffic-filter-rules-including-waf.md#recommended-starter-rules)。

如果您需要在上線期間重新校準任務，可以隨時參考該清單。
