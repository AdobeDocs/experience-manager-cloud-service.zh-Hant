---
title: Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.11.0 的發行說明
description: 以下是 AEM as a Cloud Service 中 Cloud Manager 2023.11.0 的發行說明。
feature: Release Information
exl-id: 9c73d7ab-c2c2-4803-a07b-e9054220c6b2
source-git-commit: be38ca5bf79d401fc12c1422c270a2ee84bbbad2
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 100%

---


# Adobe Experience Manager as a Cloud Service 中 Cloud Manager 2023.11.0 的發行說明 {#release-notes}

本頁面記錄了 AEM as a Cloud Service 中 Cloud Manager 版本 2023.11.0 的發行說明。

>[!NOTE]
>
>如需有關 Adobe Experience Manager as a Cloud Service 的最新發行說明，請參閱[本頁面](/help/release-notes/release-notes-cloud/release-notes-current.md)。

## 發行日期 {#release-date}

AEM as a Cloud Service 中的 Cloud Manager 版本 2023.11.0 發行日期是 2023 年 11 月 14 日。下一個版本計畫於 2023 年 12 月 7 日發行。

## 新增功能 {#what-is-new}

* Web 應用程式防火牆-DDOS 防護 (WAF-DDOS) 現在可作為 AEM as a Cloud Service 權利的一部分供購買，並且[能以自助方式進行設定。](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)
* 專業[設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)現在可在幾分鐘內設定和部署流量篩選規則，包括 WAF 規則。
* [複製內容時](/help/implementing/developing/tools/content-copy.md) (從較高環境複製到開發環境)，現在會顯示一則訊息：建議在複製大型內容集時要小心謹慎，因為開發環境的容量有限。
* [管道執行詳細資訊頁面](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)現在會顯示管道執行中的所有步驟，尚未開始的步驟呈現灰色。
* **[活動](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity)**&#x200B;和&#x200B;**[管道](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipelines)**&#x200B;頁面中，現在選取執行中管道即可取得管道執行摘要。
* [管道詳細資訊頁面](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)中已加入新的&#x200B;**持續時間**&#x200B;區段，其中包含基於該方案歷史趨勢的管道步驟平均持續時間。
* 在[管道執行頁面](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#activity-window)上，已完成的步驟現在會顯示持續時間。
* [重新使用組建成品](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/setting-up-project.md#build-artifact-reuse)的執行現在會顯示最初建置這些成品之執行的連結。
* 現在也可以為[程式碼品質管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md)設定用於選取&#x200B;**重要的量度失敗**&#x200B;的選項。


## 早期採用計劃 {#early-adoption}

若想要有機會測試一些即將推出的功能，請參加 Adobe 的早期採用者計劃。

### 帶著您自己的 GitHub {#byo-github}

如果您使用 GitHub 來管理您的存放庫，[現在您可以透過 Cloud Manager 直接在 GitHub 存放庫中驗證程式碼。](/help/implementing/cloud-manager/managing-code/byo-github.md)這種整合消除了始終將程式碼與 Adobe 存放庫保持同步的需要，並允許您先確認提取要求再將其合併到主要分支。

如果您有興趣測試此新功能並分享您的意見反應，可使用和您的 Adobe ID 相關聯的電子郵件地址傳送電子郵件至 `Grp-CloudManager_BYOG@adobe.com`。

### 自訂權限 {#custom-permissions}

[Cloud Manager 自訂權限](/help/implementing/cloud-manager/custom-permissions.md)可讓您以可設定的權限建立自訂權限設定檔，以限制 Cloud Manager 使用者對方案、管道和環境的存取。

如果您有興趣測試此新功能並分享您的意見反應，可使用和您的 Adobe ID 相關聯的電子郵件地址傳送電子郵件至 `Grp-CloudManager-custom-permissions@adobe.com`。

### 自助服務內容還原 {#content-restore}

[新的自助服務內容還原功能](/help/operations/restore.md)現在會提供最長達 7 天的備份還原，並可供早期採用者用於評估目的，其中包括：

* 前 24 小時的時間點備份還原
* 固定時間還原最長可達 7 天

如果您有興趣測試此新功能並分享您的意見反應，可使用和您的 Adobe ID 相關聯的電子郵件傳送電子郵件至 `aemcs-restorefrombackup-adopter@adobe.com`。

* 早期採用者計劃僅適用於開發環境。
* 此功能可使用的早期採用者計劃很有限。
* 此功能用於恢復意外刪除的內容，不適用於災難復原。

### 體驗稽核儀表板 {#experience-audit-dashboard}

[Cloud Manager 體驗稽核儀表板](/help/implementing/cloud-manager/experience-audit-dashboard.md)包括頁面效能分數的趨勢檢視以及可協助您提高效能分數的深入解析和建議。體驗稽核會隨附為 Cloud Manager 生產管道中的一個步驟。

該儀表板使用 Google Lighthouse，這是一種開放原始碼自動化工具，可提升網頁應用程式的品質。您可以用於在任何網頁 (公用網頁或需要身份驗證的網頁) 上執行。可用於對效能、協助工具、漸進式網頁應用程式、SEO 等進行稽核。

有興趣測試新儀表板嗎？若要開始，請使用和您的 Adobe ID 相關聯的電子郵件傳送電子郵件至 `aem-lighthouse-pilot@adobe.com`。

## 已知問題 {#known-issues}

有一個已知的錯誤會阻止[設定管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md##config-deployment-pipeline)被推至生產。

如果設定管道需要「**部署到生產前暫停**」選項管道，建議採用以下臨時措施至錯誤解決為止。

1. 執行管道.
1. 在暫存環境中測試程式碼。
1. 當部署及核准可供使用時，請按一下「**拒絕**」。
1. 編輯管道以便您可以停用「**部署到生產前暫停**」選項。
1. 再次執行管道，以便管道可以在暫存階段再次執行，然後在生產環境中執行。
