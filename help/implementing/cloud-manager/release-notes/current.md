---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.10.0 的發行說明
description: 瞭解AEM as a Cloud Service中Cloud Manager 2024.10.0的發行說明。
feature: Release Information
role: Admin
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 12%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.10.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 版本 2024.10.0 的發行說明。

>[!NOTE]
>
>請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager版本2024.10.0發行日期是2024年10月3日。

下一版本計畫於2024年11月14日發行。

## 新增功能 {#what-is-new}

* <!-- BOTH CS & AMS --> Cloud Manager中使用的AEM原型版本現在更新至版本26。 請參閱[https://github.com/adobe/aem-project-archetype/releases](https://github.com/adobe/aem-project-archetype/releases)

<!-- (CMGR-59817) -->

* <!-- CS ONLY --> 新增自訂網域時，之前的驗證方法涉及漫長的DNS驗證過程。 Adobe為客戶簡化了此程式。 現在，您只需要提供有效的SSL憑證（EV或OV），作為擁有權的證明。 不再需要更新DNS中的TXT記錄。

  >[!NOTE]
  >
  >此功能僅適用於客戶管理的EV和OV憑證。 由Adobe管理的DV憑證仍需要存在CNAME記錄。

  請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

  ![驗證客戶管理的EV/OV憑證的網域](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png)

* <!-- CS ONLY --> 當您新增或編輯網路基礎結構時，會根據下列規則驗證IP位址和網路遮罩欄位中的值：

   * 位址空間不能與連線位址空間中所定義的位址重疊。
   * DNS位址必須屬於連線位址空間中所定義的網路遮罩，或是公用。

  ![新增網路基礎結構對話方塊](/help/implementing/cloud-manager/release-notes/assets/network-infrastructure-add.png)

* <!-- CS ONLY --> 正在變更環境部署記錄的格式，以便索引、安裝可變內容和轉換工作。

  >[!NOTE]
  >
  >此變更計劃分階段推出，預期完成日期為2024年12月。

  ![部署至生產卡](/help/implementing/cloud-manager/release-notes/assets/deploy-to-production-card.png)

  記錄檔的格式將會從下列的簡單專案變更：

  ![顯示簡單專案的記錄檔](/help/implementing/cloud-manager/release-notes/assets/log-file-simple-entry.png)

  JSON專案的下列專案：

  ![記錄檔顯示json專案](/help/implementing/cloud-manager/release-notes/assets/log-file-json-entry.png)


## 早期採用方案 {#early-adoption}

成為Cloud Manager早期採用計畫的一部分，並有機會測試即將推出的功能。

### 自備Git — 現在支援GitLab和Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**自攜Git**&#x200B;功能已擴充為包含對外部存放庫（例如GitLab和Bitbucket）的支援。 除了這項新支援之外，私人和企業GitHub存放庫也提供現有支援。 新增這些新存放庫時，您也可以將其直接連結至您的管道。 您可以在公用雲端平台上或您的私人雲端或基礎架構內託管這些存放庫。 此整合也免除了與Adobe存放庫持續進行程式碼同步的需求，並可讓您在將提取請求合併至主要分支之前先驗證提取請求。

請參閱[在Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md)中新增外部存放庫。

![新增存放庫對話框](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>目前，GitHub託管的存放庫僅能執行現成可用的提取要求程式碼品質檢查，不過也正在研究更新以將此功能擴充至其他Git廠商。

如果您有興趣測試這項新功能並分享您的意見回饋，請從與Adobe ID相關聯的電子郵件地址傳送電子郵件至[Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com)。 請務必加入您要使用的Git平台，以及您是要使用私人/公有或企業存放庫結構。


<!-- ## Bug fixes




## Known issues {#known-issues} -->
