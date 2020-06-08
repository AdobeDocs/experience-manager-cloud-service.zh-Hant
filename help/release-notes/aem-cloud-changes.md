---
title: Adobe Experience Manager (AEM) 雲端服務重大變更
description: Adobe Experience Manager (AEM) 雲端服務重大變更
translation-type: tm+mt
source-git-commit: e76de9b84931dced6383570e384ffdb6fb334daf
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 100%

---


# Adobe Experience Manager (AEM) 雲端服務重大變更 {#notable-changes-aem-cloud}

AEM 雲端服務提供許多管理 AEM 專案的新功能，並帶來許多可能性。但 AEM 雲端服務與 AEM Sites 內部部署或 Adobe 受管服務之間仍有許多差異。本文件主要說明這些重要差異。

>[!NOTE]
>本文件著重說明 AEM 整體的重大變更。若需了解特定解決方案的變更項目，請參閱：
>
>* [AEM 雲端服務中 AEM Sites 的重大變更](/help/sites-cloud/sites-cloud-changes.md)
>* [AEM 雲端服務中 AEM Assets 的重大變更](/help/assets/assets-cloud-changes.md)


主要差異在於以下方面：

* [/apps 和 /libs 在執行階段不可修改](#apps-libs-immutable)
* [OSGi 套件和設定必須依儲存庫為準](#osgi)
* [禁止變更發佈用儲存庫](#changes-to-publish-repo)
* [禁止自訂執行模式](#custom-runmodes)
* [移除複寫代理](#replication-agents)
* [移除傳統 UI](#classic-ui)
* [發佈端傳送](#publish-side-delivery)
* [資產處理與傳送](#asset-handling)

## /apps 和 /libs 在執行階段不可修改 {#apps-libs-immutable}

`/apps` 和 `/libs` 中的所有內容和子資料夾均為唯讀。任何預期能變更的功能或自訂程式碼都將無法變更。系統會傳回此類內容為唯讀、寫入作業無法完成的錯誤。AEM 的許多地方都會受到影響：

* 完全禁止變更 `/libs`。
   * 這不是新規則，但內部部署的舊版 AEM 並未強制執行此規則。
* `/libs` 中允許重疊的區域覆蓋仍可在 `/apps` 內使用。
   * 此類覆蓋必須透過 CI/CD 管道從 Git 取得。
* 無法透過 UI 編輯儲存於 `/apps` 的靜態範本設計資訊。
   * 建議您改用可編輯的範本。
   * 如果仍需靜態範本，則須透過 CI/CD 管道從 Git 取得設定資訊。
* MSM Blueprint 和自訂 MSM 轉出設定必須透過 CI/CD 管道從 Git 安裝。
* 若要變更 I18n 翻譯，須透過 CI/CD 管道從 Git 執行。

## OSGi 套件和設定必須依儲存庫為準 {#osgi}

舊版 AEM 中用於變更 OSGi 設定的 Web 主控台，無法在 AEM 雲端服務中使用。因此，若要變更 OSGi，必須透過 CI/CD 管道執行。

* 只能透過 Git 持續性變更 OSGi 設定，作為 JCR 型 OSGi 設定使用。
* 全新或更新的 OSGi 套件必須在 CI/CD 管道建置程序中透過 Git 導入。

## 禁止變更發佈用儲存庫 {#changes-to-publish-repo}

AEM 雲端服務禁止直接變更發佈用儲存庫。在舊版內部部署 AEM 或 AMS 上的 AEM 中，可直接變更發佈用儲存庫的程式碼，以建立使用者、更新使用者設定檔及建立節點。現在已無法這麼做，但可透過下列方式緩解：

* 內容和以內容為基礎的設定：變更作者例項並發佈。
* 程式碼和設定：在 GIT 儲存庫中變更，並執行 CI/CD 管線以轉出這些變更。
* 使用者相關資料 (例如提交的表單或設定檔資料)：使用 Experience Cloud Platform 或其他第三方工作階段感知存放區的統一設定檔服務。

## 禁止自訂執行模式 {#custom-runmodes}

AEM 雲端服務提供以下現成執行模式：

* `author`
* `publish`
* `prod`
* `author.prod`
* `publish.prod`
* `stage`
* `author.stage`
* `publish.stage`
* `dev`
* `author.dev`
* `publish.dev`

AEM 雲端服務無法使用其他或自訂的執行模式。

## 移除複寫代理 {#replication-agents}

在 AEM 雲端服務中，內容是使用 [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) 發佈。舊版 AEM 不再使用或提供複寫代理，這可能會影響現有 AEM 專案的下列作業：

* 例如，將內容推送至預覽伺服器複寫代理的自訂工作流程。
* 自訂複寫代理以轉換內容
* 使用「反向複寫」將內容從發佈階段撤回給作者

## 移除傳統 UI {#classic-ui}

AEM 雲端服務不再提供傳統 UI。

## 發佈端傳送 {#publish-side-delivery}

AEM 雲端服務預設啟用 HTTP 加速功能，包括適用於作者與發佈服務的 CDN 和流量管理。

若是從 AMS 或內部部署轉換的專案，Adobe 強烈建議使用內建的 CDN，因為 AEM 雲端服務中的功能已針對提供的 CDN 最佳化。

## 資產處理與傳送 {#asset-handling}

AEM 雲端服務已最佳化上傳、處理和下載資產的相關作業，以更有效率地執行擴展功能，並加快上傳和下載速度。然而，這可能會影響部分現有的自訂程式碼。

* 舊版 AEM 已不提供預設的工作流程 **DAM Asset Update**。
* 若要&#x200B;**在不轉換的情況下**&#x200B;傳送二進位的網站元件，應使用直接下載。
   * Sling GET servlet 已變更為預設執行此動作。
* **在轉換的情況下**&#x200B;傳送二進位的網站元件 (例如透過 servlet 調整大小) 仍可繼續運作。
* 若是透過封裝管理程式傳入資產，須使用 Assets 介面中的&#x200B;**「重新處理資產」**&#x200B;動作，手動重新處理。
