---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.4.0 的發行說明
description: 了解 AEM as a Cloud Service 中 Cloud Manager 2025.4.0 的發行資訊。
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 6dc92a0f824ca9bc3726b48581ace232302691e5
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 60%

---

# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2025.4.0 的發行說明 {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

了解 AEM (Adobe Experience Manager) as a Cloud Service 中 Cloud Manager 2025.4.0 的發行資訊。


另請參閱 [Adobe Experience Manager as a Cloud Service 最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service中的Cloud Manager 2025.4.0發行日期是2025年4月10日星期四。

下一個預計發行日期為2025年5月8日星期四。

## 最新資訊 {#what-is-new}

* **(UI)已改善部署可見性**

  當部署等待另一個部署完成時，Cloud Manager中的管道執行詳細資訊頁面現在會顯示狀態訊息（&quot;*正在等待 — 其他更新進行中*&quot;）。 此工作流程可讓您更容易瞭解環境部署期間的排序。 <!-- CMGR-66890 -->

  ![顯示詳細資訊和劃分的開發部署對話方塊](/help/implementing/cloud-manager/release-notes/assets/dev-deployment.png)

* **(UI)網域驗證增強功能**

  新增網域時，如果網域已安裝在Fastly帳戶中，Cloud Manager現在會顯示錯誤： &quot;*網域已安裝在Fastly帳戶中。 請先將它從此處移除，然後再新增至Cloud Service。*」

## 早期採用方案 {#early-adoption}

參與Cloud Manager的搶先採用計畫，在即將推出的功能正式發行前取得獨家存取權。

目前提供下列早期採用機會：

### 自備 Git - 現在支援 GitLab 和 Bitbucket {#gitlab-bitbucket}

<!-- BOTH CS & AMS -->

**自備 Git** 功能已擴充，以納入對 GitLab 和 Bitbucket 等外部存放庫的支援。這項新的支援功能是對私人和企業 GitHub 存放庫現有支援的補充。當您新增這些新存放庫時，也可以將它們直接連結到您的管道。您可以將這些存放庫託管在公有雲平台上或私有雲或基礎架構內。這項整合也消除了與 Adobe 存放庫持續進行代碼同步的需求，並提供了在提取請求合併到主分支之前，驗證提取請求的功能。

對於使用外部存放庫 (不包括 GitHub 託管的存放庫) 且&#x200B;**部署觸發程序**&#x200B;設定為「**在 Git 變更時**」的管道，現在會自動啟動。

請查看[在 Cloud Manager 中新增外部存放庫](/help/implementing/cloud-manager/managing-code/external-repositories.md)。

![新增存放庫對話框](/help/implementing/cloud-manager/release-notes/assets/repositories-add-release-notes.png)

>[!NOTE]
>
>目前，立即可用的提取請求代碼品質檢查僅限於 GitHub 託管的存放庫，但我們正在進行一項更新以將此功能擴展到其他 Git 供應商。

如果您有興趣測試此新功能並分享您的意見回饋，請使用與您的 Adobe ID 關聯的電子郵件地址向 [Grp-CloudManager_BYOG@adobe.com](mailto:Grp-CloudManager_BYOG@adobe.com) 傳送電子郵件。請務必包含您要使用的 Git 平台以及您是否使用私人/公開或企業存放庫結構。

### AEM 首頁 {#aem-home}

AEM 首頁推出一個集中化的起點，用於在 Adobe Experience Manager 中管理內容、資產和網站。AEM 首頁旨在提供個人化體驗，可讓您根據自己的角色和目標順暢地導覽 AEM 生態系統。它以指南的方式提供關鍵的深入解析和建議的動作，協助您有效率地達成目標。AEM 首頁具備以角色為導向的清晰版面，確保快速存取基本工具，有助於在所有 AEM 功能中提供簡化且有效的體驗。

AEM 首頁可供早期採用者使用，提供專注於提升工作流程、確定目標優先順序和交付結果的最佳化體驗。如果選擇加入，您可以提供回饋意見來影響 AEM 首頁的開發，協助塑造其未來並提升其對整個 AEM 社群的價值。

如果您有興趣測試這個新功能並分享回饋意見，請使用與您的 Adobe ID 相關聯的電子郵件地址寄送電子郵件至 [Grp-AemHome@adobe.com](mailto:Grp-AemHome@adobe.com)。請務必包含以下資訊：

* 最適合您個人資料的角色：內容作者、開發人員、業務負責人、管理員或其他 (請提供說明)。
* 您的主要 AEM 存取表面：AEM Sites、AEM Assets、AEM Forms、Cloud Manager 或其他 (請提供說明)。

## 錯誤修正

* **憑證遺失一般名稱(CN)欄位的問題**

  處理主旨欄位中未包含一般名稱(CN)的EV/OV憑證時，Cloud Manager不再擲回NullPointerException (NPE)和500 HTTP回應。 現代憑證通常會省略CN，改用主體替代名稱(SAN)。 此修正可確保在SAN存在時，CN的缺失不會再導致組態建置流程失敗。<!-- CMGR-67548 -->

* **網域驗證問題，憑證比對不正確**

  Cloud Manager不再使用錯誤的憑證來錯誤驗證網域。 以前，驗證邏輯使用以模式為基礎的比對，而非完全比對，這會導致`should-not-be-verified.example.com`之類的網域因為與`example.com`的有效憑證重疊而顯示為已驗證。 此修正確保網域驗證現在會檢查完全符合的專案，以防止錯誤的憑證關聯。<!-- CMGR-67225 -->

* **進階網路連線埠轉寄名稱的強制唯一性**

  Cloud Manager現在對進階網路連線埠轉送強制執行唯一命名。 之前允許使用重複的名稱，這可能會導致衝突。 此修正可確保每個連線埠轉送專案都有不同的名稱，符合網路組態完整性的最佳實務。<!-- CMGR-67082 -->


<!-- ## Known issues {#known-issues} -->

