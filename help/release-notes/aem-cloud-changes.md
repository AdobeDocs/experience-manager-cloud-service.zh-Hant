---
title: Adobe Experience Manager (AEM) as a Cloud Service 重大變更
description: Adobe Experience Manager (AEM) as a Cloud Service 重大變更.
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 50%

---

# Adobe Experience Manager as a Cloud Service重大變更 {#notable-changes-aem-cloud}

Adobe Experience Manager (AEM)Cloud Service提供許多管理AEM專案的新功能，並帶來許多可能性。 不過，與AEM Cloud Service相比，AEM Sites內部部署或Adobe受管服務之間有一些差異。 本文件主要說明這些重要差異。

>[!CONTEXTUALHELP]
>id="aem_cloud_notable_changes"
>title="AEM as a Cloud Service 重大變更"
>abstract="在此標籤中，您可以檢視有助於了解 AEM 內部部署或 Adobe Managed Services 與 AEM as a Cloud Service 之間差異的內容。"
>additional-url="https://video.tv.adobe.com/v/330543" text="AEM as a Cloud Service 的演進"


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

* [OSGi 套件組合和設定必須視為程式碼](#osgi)

* [禁止變更發佈用儲存庫](#changes-to-publish-repo)

* [不允許自訂執行模式](#custom-runmodes)

* [移除複寫代理程式和相關變更](#replication-agents)

* [移除傳統 UI](#classic-ui)

* [發佈端傳送](#publish-side-delivery)

* [資產處理與傳送](#asset-handling)

## /apps 和 /libs 在執行階段不可修改 {#apps-libs-immutable}

中的任何內容和子資料夾 `/apps` 和 `/libs` 是唯讀的。 任何預期會在該處進行變更的功能或自訂程式碼都將無法變更。 系統會傳回此類內容為唯讀、寫入作業無法完成的錯誤。這對AEM的多個領域都有影響：

* 完全禁止變更 `/libs`。
   * 這不是新規則，但內部部署的舊版AEM並未強制執行此規則。
* 中的區域覆蓋 `/libs` 可以覆蓋的仍允許在 `/apps`.
   * 此類覆蓋必須透過CI/CD管道從Git取得。
* 儲存於中的靜態範本設計資訊 `/apps` 無法透過UI編輯。
   * 建議您改用可編輯的範本。
   * 如果仍需靜態範本，則須透過CI/CD管道從Git取得設定資訊。
* 必須透過CI/CD管道從Git安裝MSM Blueprint和自訂MSM轉出設定。
* 必須透過CI/CD管道從Git變更I18n翻譯。

## OSGi 套件組合和設定必須視為程式碼 {#osgi}

對OSGi套件組合和設定的變更必須透過CI/CD管道引入。

* 全新或更新的OSGi套件組合必須透過Git透過CI/CD管道引入。
* 只能透過CI/CD管道從Git變更OSGi設定。

舊版 AEM 中用於變更 OSGi 套件組合和設定的 Web 主控台，無法在 AEM Cloud Service 中使用。

## 禁止變更發佈用存放庫 {#changes-to-publish-repo}

除了在發佈層上 `/home` 資料夾下的變更，不允許在 AEM Cloud Service 上直接變更發佈存放庫。在內部部署 AEM 或 AMS 上的 AEM 的早期版本中，可以直接對發佈存放庫進行程式碼變更。可以透過以下方式減緩一些限制：

* 內容和內容型設定：在Author例項上進行變更並發佈。
* 程式碼和設定：在GIT存放庫中進行變更，並執行CI/CD管道以轉出這些變更。

## 不允許自訂執行模式 {#custom-runmodes}

AEM Cloud Service提供下列立即可用的執行模式：

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

AEM Cloud Service 無法使用其他或自訂的執行模式。

## 移除複寫代理程式和相關變更 {#replication-agents}

在 AEM Cloud Service 中，內容是使用 [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) 發佈。舊版AEM不再使用或提供復寫代理，這可能會影響現有AEM專案的下列作業：

* 例如，將內容推送至預覽伺服器複寫代理的自訂工作流程。
* 自訂複寫代理以轉換內容.
* 使用「反向復寫」將內容從「發佈」帶回「作者」。

此外，暫停和停用按鈕也會從復寫代理程式管理控制檯中移除。

## 移除傳統 UI {#classic-ui}

AEM Cloud Service 不再提供傳統 UI。

## 發佈端傳送 {#publish-side-delivery}

AEM Cloud Service預設啟用HTTP加速功能，包括適用於作者與發佈服務的CDN和流量管理。

若是從AMS或內部部署轉換的專案，Adobe強烈建議使用內建的CDN，因為AEM Cloud Service中的功能已針對提供的CDN最佳化。

## 資產處理與傳送 {#asset-handling}

資產上傳、處理和下載已在 [!DNL Experience Manager Assets] as a [!DNL Cloud Service] 中最佳化。AEM [!DNL Assets] 現在效率更高，支援更多調整，並讓您以更快的速度上傳和下載。 此外，它還會影響現有的自訂程式碼和一些作業。如需各項變更以及與 [!DNL Experience Manager]6.5 功能配對的清單，請參閱 [ [!DNL Assets]](/help/assets/assets-cloud-changes.md) 變更。
