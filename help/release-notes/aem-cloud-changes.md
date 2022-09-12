---
title: Adobe Experience Manager (AEM) as a Cloud Service 重大變更
description: Adobe Experience Manager (AEM) as a Cloud Service 重大變更
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
source-git-commit: d3208a9a0785909e9b62d4033437a8ff44f7ba3e
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 66%

---

# Adobe Experience Manager (AEM) as a Cloud Service 重大變更 {#notable-changes-aem-cloud}

AEM 雲端服務提供許多管理 AEM 專案的新功能，並帶來許多可能性。但 AEM 雲端服務與 AEM Sites 內部部署或 Adobe 受管服務之間仍有許多差異。本文件主要說明這些重要差異。

>[!CONTEXTUALHELP]
>id="aem_cloud_notable_changes"
>title="AEMas a Cloud Service中重大變更"
>abstract="在此標籤中，您可以檢視有助於您了解內部部署AEM或Adobe Managed Services之間差異的內容，與AEMas a Cloud Service比較。"
>additional-url="https://video.tv.adobe.com/v/330543" text="AEMas a Cloud Service的演變"


>[!NOTE]
>本文件著重說明 AEM 整體的重大變更。如需詳細資訊和解決方案的特定變更，請參閱：
>
>* [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)
>* Adobe Experience Manager as a Cloud Service 與舊版的[新增功能與不同之處](/help/overview/what-is-new-and-different.md)
>* Adobe Experience Manager as a Cloud Service [架構](/help/overview/architecture.md)
>* [AEM Sites as a Cloud Service 重大變更](/help/sites-cloud/sites-cloud-changes.md)
>* [AEM Assets as a Cloud Service 重大變更](/help/assets/assets-cloud-changes.md)


主要差異在於以下方面：

* [/apps 和 /libs 在執行階段不可修改](#apps-libs-immutable)

* [OSGi套件和設定必須視為程式碼](#osgi)

* [禁止變更發佈用儲存庫](#changes-to-publish-repo)

* [禁止自訂執行模式](#custom-runmodes)

* [移除復寫代理及相關變更](#replication-agents)

* [移除傳統 UI](#classic-ui)

* [發佈端傳送](#publish-side-delivery)

* [資產處理與傳送](#asset-handling)

## /apps 和 /libs 在執行階段不可修改 {#apps-libs-immutable}

`/apps` 和 `/libs` 中的所有內容和子資料夾均為唯讀。任何預期能變更的功能或自訂程式碼都將無法變更。系統會傳回此類內容為唯讀、寫入作業無法完成的錯誤。AEM 的許多地方都會受到影響：

* 完全禁止變更 `/libs`。
   * 這不是新規則，但內部部署的舊版 AEM 並未強制執行此規則。
* 中區域的覆蓋 `/libs` 允許重疊的 `/apps`.
   * 此類覆蓋必須透過 CI/CD 管道從 Git 取得。
* 無法透過 UI 編輯儲存於 `/apps` 的靜態範本設計資訊。
   * 建議您改用可編輯的範本。
   * 如果仍需靜態範本，則須透過 CI/CD 管道從 Git 取得設定資訊。
* MSM Blueprint 和自訂 MSM 轉出設定必須透過 CI/CD 管道從 Git 安裝。
* 若要變更 I18n 翻譯，須透過 CI/CD 管道從 Git 執行。

## OSGi套件和設定必須視為程式碼 {#osgi}

必須透過CI/CD管道導入OSGi套件組合和組態的變更。

* 必須透過CI/CD管道透過Git導入新的或更新的OSGi套件組合。
* 只能透過CI/CD管道從Git變更OSGi設定。

舊版AEM中用於變更OSGi套件組合和設定的Web主控台，在AEM Cloud Service中無法使用。

## 禁止變更發佈用儲存庫 {#changes-to-publish-repo}

除了 `/home` 資料夾，則AEM Cloud Service不允許直接變更發佈存放庫。 在舊版內部部署AEM或AMS上的AEM中，程式碼可直接變更發佈用存放庫。 可透過下列方式緩解部分限制：

* 內容和以內容為基礎的設定：變更作者例項並發佈。
* 程式碼和設定：在 GIT 儲存庫中變更，並執行 CI/CD 管線以轉出這些變更。

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

## 移除復寫代理及相關變更 {#replication-agents}

在 AEM 雲端服務中，內容是使用 [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) 發佈。舊版 AEM 不再使用或提供複寫代理，這可能會影響現有 AEM 專案的下列作業：

* 例如，將內容推送至預覽伺服器複寫代理的自訂工作流程。
* 自訂複寫代理以轉換內容
* 使用「反向複寫」將內容從發佈階段撤回給作者

此外，請注意，暫停和停用按鈕已從復寫代理管理控制台中移除。

## 移除傳統 UI {#classic-ui}

AEM 雲端服務不再提供傳統 UI。

## 發佈端傳送 {#publish-side-delivery}

AEM 雲端服務預設啟用 HTTP 加速功能，包括適用於作者與發佈服務的 CDN 和流量管理。

若是從 AMS 或內部部署轉換的專案，Adobe 強烈建議使用內建的 CDN，因為 AEM 雲端服務中的功能已針對提供的 CDN 最佳化。

## 資產處理與傳送 {#asset-handling}

資產上傳、處理和下載都可在 [!DNL Experience Manager Assets] as a [!DNL Cloud Service]. [!DNL Assets] 現在更有效率、更能擴充，並且讓您以更快的速度上傳和下載。 此外，這也會影響現有的自訂程式碼和某些操作。 以取得變更清單，並與 [!DNL Experience Manager] 6.5功能，請參閱 [變更 [!DNL Assets]](/help/assets/assets-cloud-changes.md).
