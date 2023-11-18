---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.11.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2023.11.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 60%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.11.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 版本 2023.11.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2023.11.0 發行日期是 2023 年 11 月 14 日。下一個版本計畫於 2023 年 12 月 7 日發行。

## 新增功能 {#what-is-new}

* Web應用程式防火牆 — DDOS保護(WAF-DDOS)現在可作為AEMas a Cloud Service許可權的一部分購買，並且 [能以自助方式設定。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* 專門化 [設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 現在可在數分鐘內設定和部署流量篩選規則，包括WAF規則。
* [複製內容時](/help/implementing/developing/tools/content-copy.md) 從更高的環境到開發環境，現在會顯示一則訊息，建議在複製大型內容集時務必謹慎，因為開發環境存在容量限制。
* [管道執行詳細資訊頁面](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)現在將顯示管道執行中的所有步驟，尚未開始的步驟呈現灰色。
* **[活動](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity)**&#x200B;和&#x200B;**[管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines)**&#x200B;頁面中，現在按一下執行中管道即可取得管道執行摘要。
* [管道詳細資訊頁面](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)中已加入新的&#x200B;**持續時間**&#x200B;區段，其中包含基於該方案歷史趨勢的管道步驟平均持續時間。
* 在 [管道執行頁面，](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity-window) 完成的步驟現在會顯示持續時間。
* 執行次數： [重複使用組建成品](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse) 現在將顯示最初建立這些成品的執行連結。
* 要選取的選項 **重要量度失敗** 現在可以設定為 [計畫碼品質管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md) 以及。


## 早期採用計劃 {#early-adoption}

參加我們的早期採用計劃，即有機會測試一些即將推出的功能。

### 帶著您自己的 GitHub {#byo-github}

如果您使用 GitHub 來管理您的存放庫，[現在您可以透過 Cloud Manager 直接在 GitHub 存放庫中驗證程式碼。](/help/implementing/cloud-manager/managing-code/byo-github.md)這種整合消除了始終將程式碼與 Adobe 存放庫保持同步的需要，並允許您先確認提取要求再將其合併到主要分支。

如果您有興趣測試這項新功能並分享您的回饋意見，請傳送電子郵件至 `Grp-CloudManager_BYOG@adobe.com` 來自與Adobe ID相關聯的電子郵件地址。

### 自訂權限 {#custom-permissions}

[Cloud Manager 自訂權限](/help/implementing/cloud-manager/custom-permissions.md)允許您以可設定的權限建立新的自訂權限設定檔，以限制 Cloud Manager 使用者對程式、管道和環境的存取。

如果您有興趣測試這項新功能並分享您的回饋意見，請傳送電子郵件至 `Grp-CloudManager-custom-permissions@adobe.com` 來自與Adobe ID相關聯的電子郵件地址。

### 自助服務內容還原 {#content-restore}

[新的自助服務內容還原功能](/help/operations/restore.md)現在會提供最長達 7 天的備份還原，並可供早期採用者用於評估目的，其中包括：

* 前 24 小時的時間點備份還原
* 固定時間還原最長可達 7 天

如果您有興趣測試這項新功能並分享您的回饋意見，請傳送電子郵件至 `aemcs-restorefrombackup-adopter@adobe.com` 從與您的Adobe ID相關聯的電子郵件中。

* 早期採用者計劃僅適用於開發環境。
* 此功能可使用的早期採用者計劃很有限。
* 此功能用於恢復意外刪除的內容，不適用於災難復原。

### 體驗稽核儀表板 {#experience-audit-dashboard}

[Cloud Manager 體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括頁面效能分數的趨勢檢視以及可協助您提高效能分數的深入解析和建議。體驗稽核會隨附為 Cloud Manager 生產管道中的一個步驟。

該儀表板會利用 Google Lighthouse，這是一種開放原始碼自動化工具，用於提高網頁應用程式的品質。您可以用於在任何網頁 (公用網頁或需要身份驗證的網頁) 上執行。可用於對效能、協助工具、漸進式網頁應用程式、SEO 等進行稽核。

有興趣測試新儀表板嗎？傳送電子郵件至 `aem-lighthouse-pilot@adobe.com` 從與Adobe ID相關聯的電子郵件中，我們可以協助您開始使用。

## 已知問題 {#known-issues}

有一個已知的Bug防止 [設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md##config-deployment-pipeline) 以免推送至生產環境。

如果 **在部署到生產之前暫停** 選項是設定管道的必要專案，以下是在解決錯誤之前建議的因應措施。

1. 執行管道.
1. 在中繼環境中測試程式碼。
1. 部署並取得核準時，按一下 **拒絕**.
1. 編輯管道以停用 **在部署到生產之前暫停** 選項。
1. 再次執行管道。 它將在測試上再次執行，然後在生產上執行。
