---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.12.0 的發行說明
description: 了解 AEM as a Cloud Service 中 Cloud Manager 2024.12.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 8e89adcaadbc53c3d525d57ef452f671137a619f
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 42%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2024.12.0 的發行說明 {#release-notes}

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2024.12.0 的發行資訊。

>[!NOTE]
>
>請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2024.12.0發行日期是2024年12月5日星期四。

下一個預計發行日期為2025年1月23日。


## 新增功能 {#what-is-new}

<!-- * **Java 21 support:** Customers can now optionally build with Java 17 or Java 21, benefiting from performance improvements and new language features. See [Build environment](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) for configuration steps, including updating your Maven project description, and certain library versions. When the build version is set to Java 17 or Java 21, the runtime defaults to Java 21.

    Starting February 2025, sandboxes and dev environments upgrade to the Java 21 runtime, regardless of the build version (Java 8, 11, 17, or 21). Production environments follow with an upgrade in April 2025. -->

* **已新增A記錄型別：**&#x200B;對A記錄型別的支援，以使用AEM Cloud Manager中的CDN設定來改善網域的上線整備。 您現在可以選擇新增CNAME記錄型別或代表Fastly的IP的A記錄型別來上線，以簡化網域路由。 此增強功能消除了僅依賴CNAME記錄進行Fastly網域設定的限制。

  請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。<!-- CMGR-63076 -->

<!-- * The AEM Code Quality step now uses SonarQube 9.9 Server, replacing the older 7.4 version. This upgrade brings additional security, performance, and code quality checks, offering more comprehensive analysis and coverage for your projects. -->

* **將多個網域新增至Edge Delivery網站：**&#x200B;您現在可以在AEM Cloud Manager中將多個網域（包括Apex及非Apex網域）新增至Edge Delivery網站(EDS)。 此增強功能解決了先前限制將多個網域與EDS來源建立關聯的能力限制。 此更新可確保更靈活地管理網域設定，並簡化具有複雜網域設定的網站的上線流程。<!-- CMGR-63007 -->

* **進階篩選選項：**&#x200B;已在AEM Cloud Manager的管道執行頁面和SSL憑證頁面上引入進階篩選選項。 您現在可以依多個條件進行篩選，讓您更快速地存取相關資料，並提高部署效率。<!-- CMGR-26263 -->

   * **管道活動篩選：**包含管道活動篩選，讓您精簡特定管道活動的搜尋結果。 可用的篩選器包括管道、動作和狀態。
     ![管道活動篩選](/help/implementing/cloud-manager/assets/filters-pipeline.png)


   * **SSL憑證篩選：**包含SSL憑證篩選，讓您精簡特定憑證的搜尋結果。 可用的篩選器包括SSL憑證名稱、擁有權和狀態。
     ![SSL憑證篩選](/help/implementing/cloud-manager/assets/filters-ssl-certificates.png)

## 早期採用方案 {#early-adoption}

成為 Cloud Manager 早期採用方案的一部分，並有機會測試即將推出的功能。

### 自備 Git - 現在支援 GitLab 和 Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**自備Git**&#x200B;功能已擴充為包含對外部存放庫（例如GitLab和Bitbucket）的支援。 這項新的支援功能是對私人和企業 GitHub 存放庫現有支援的補充。當您新增這些新存放庫時，也可以將它們直接連結到您的管道。您可以將這些存放庫託管在公有雲平台上或私有雲或基礎架構內。這項整合也消除了與 Adobe 存放庫持續進行代碼同步的需求，並提供了在提取請求合併到主分支之前，驗證提取請求的功能。

使用外部存放庫（不包括GitHub託管的存放庫）且&#x200B;**部署觸發程式**&#x200B;設為&#x200B;**在Git變更上**&#x200B;的管道現在會自動啟動。

請查看[在 Cloud Manager 中新增外部存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![新增存放庫對話框](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>目前，立即可用的提取請求代碼品質檢查僅限於 GitHub 託管的存放庫，但我們正在進行一項更新以將此功能擴展到其他 Git 供應商。

如果您有興趣測試此新功能並分享您的意見回饋，請使用與您的 Adobe ID 關聯的電子郵件地址向 [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) 傳送電子郵件。請務必包含您要使用的 Git 平台以及您是否使用私人/公開或企業存放庫結構。

## 錯誤修正

* 已新增保護機制，以防止刪除在AEM Cloud Manager中具有作用中網域對應的網域。 嘗試刪除這類網域的使用者現在會收到錯誤訊息，指示他們先刪除網域對應，然後再繼續刪除網域。 此工作流程可確保網域完整性並防止意外錯誤設定。<!-- CMGR-63033 -->
* 少數情況下，使用者無法新增網域名稱或更新SSL憑證，因為個別案例中的相關狀態不正確。<!-- CMGR-62816 -->


<!-- ## Known issues {#known-issues} -->
