---
title: Adobe Experience Manager(AEM)雲端服務的顯著變更
description: Adobe Experience Manager(AEM)雲端服務的顯著變更
translation-type: tm+mt
source-git-commit: e76de9b84931dced6383570e384ffdb6fb334daf

---


# Adobe Experience Manager(AEM)雲端服務的顯著變更 {#notable-changes-aem-cloud}

AEM Cloud service為管理AEM專案提供許多新功能和可能。 不過，與AEM cloud服務相比，AEM Sites在內部部署或Adobe Managed service中有許多不同。 本檔案強調重要的差異。

>[!NOTE]
>本檔案著重說明AEM整體的顯著變更。 如需解決方案特定的變更，請參閱：
>
>* [AEM cloud服務中AEM網站的顯著變更](/help/sites-cloud/sites-cloud-changes.md)
>* [AEM cloud服務中AEM資產的顯著變更](/help/assets/assets-cloud-changes.md)


主要差異在以下方面：

* [/apps和/libs在執行時期是不可變的](#apps-libs-immutable)
* [OSGi捆綁包和設定必須基於儲存庫](#osgi)
* [不允許對發佈儲存庫進行更改](#changes-to-publish-repo)
* [不允許自訂執行模式](#custom-runmodes)
* [刪除複製代理](#replication-agents)
* [移除傳統UI](#classic-ui)
* [發佈端傳送](#publish-side-delivery)
* [資產處理與傳送](#asset-handling)

## /apps和/libs在執行時期是不可變的 {#apps-libs-immutable}

和中的任何內容和子 `/apps` 資料夾 `/libs` 都是只讀的。 任何預期要進行變更的功能或自訂程式碼都無法進行變更。 會傳回此類內容為唯讀且寫入作業無法完成的錯誤。 這在AEM的許多領域都有影響：

* 完全不 `/libs` 允許更改。
   * 這不是新規則，不過在舊版AEM的內部部署版本中並未執行此規則。
* 允許覆蓋的 `/libs` 區域中的覆蓋仍允許在內 `/apps`。
   * 此類覆蓋必須透過CI/CD管道從Git取得。
* 無法透過UI編輯儲存在中 `/apps` 的靜態範本設計資訊。
   * 建議您改用可編輯的範本。
   * 如果仍需要靜態範本，則配置資訊必須透過CI/CD管道來自Git。
* MSM Blueprint和自訂MSM推出組態必須透過CI/CD管道從Git安裝。
* I18n翻譯更改需要通過CI/CD管道從Git進行。

## OSGi捆綁包和設定必須基於儲存庫 {#osgi}

AEM cloud服務中不提供Web Console（用於舊版AEM以變更OSGi設定）。 因此，必須通過CI/CD管線引入對OSGi的更改。

* 對OSGi設定的變更只能透過Git永續性做為JCR架構的OSGi設定。
* 新的或更新的OSGi捆綁包必須通過Git作為CI/CD管道構建過程的一部分引入。

## 不允許對發佈儲存庫進行更改 {#changes-to-publish-repo}

AEM Cloud服務不允許直接變更發佈儲存庫。 在舊版的內部部署AEM或AEM on AMS中，程式碼變更可直接對發佈儲存庫進行，例如建立使用者、更新使用者設定檔和建立節點。 這已不再可能，可以通過以下方式減輕：

* 針對以內容和內容為基礎的設定：在作者實例上進行變更並發佈。
* 對於代碼和配置：在GIT儲存庫中進行更改，然後運行CI/CD管線以推廣這些更改。
* 針對使用者相關資料，例如表單提交或描述檔資料：使用Experience Cloud Platform或其他協力廠商作業感知商店的統一描述檔服務。

## 不允許自訂執行模式 {#custom-runmodes}

AEM cloud服務現成可用的執行模式如下：

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

AEM Cloud service不提供其他或自訂的執行模式。

## 刪除複製代理 {#replication-agents}

在AEM Cloud Service中，內容是使用 [Sling Content Distribution發佈](https://sling.apache.org/documentation/bundles/content-distribution.html)。 舊版AEM中使用的複製代理不再使用或提供，這可能會影響現有AEM專案的下列區域：

* 例如將內容推送至預覽伺服器的複製代理的自訂工作流程。
* 定制到複製代理以轉換內容
* 使用「反向複製」將內容從發佈帶回作者

## 移除傳統UI {#classic-ui}

AEM Cloud service不再提供Classic UI。

## 發佈端傳送 {#publish-side-delivery}

AEM cloud服務預設會提供HTTP加速，包括CDN和作者與發佈服務的流量管理。

對於從AMS或內部安裝轉換專案，Adobe強烈建議運用內建CDN，因為AEM Cloud service中的功能已針對提供的CDN最佳化。

## 資產處理與傳送 {#asset-handling}

AEM cloud服務已最佳化資產上傳、處理和下載，讓資產更有效率，讓您更有效率地擴充資產，並加快上傳和下載。 不過，這可能會影響一些現有的自訂程式碼。

* 舊版AEM中 **的預設工作流程** DAM Asset Update已不再提供。
* 提供二進位且無變形的網站 **元件** ，應使用直接下載。
   * Sling GETservlet已變更為依預設執行。
* 透過轉換傳遞二進位檔 **案的網站元件** （例如，透過servlet調整大小）可以繼續運作。
* 透過Package manager傳入的資產需要使用「資產」介面中的「重新處 **理資產** 」動作手動重新處理。
