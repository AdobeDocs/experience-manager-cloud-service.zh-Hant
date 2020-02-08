---
title: 已知問題
description: Adobe Experience Manager雲端服務已知問題的發行說明
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 已知問題 {#known-issues}

本文將Adobe Experience manager的已知問題列為雲端服務方案。 此清單會隨Experience Manager的每個持續版本而修訂和更新。

[請連絡支援](https://helpx.adobe.com/support/experience-manager.html) ，以取得有關已知問題的詳細資訊。

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## 資產 {#assets}

<!-- Jira label: assets-cloud-known-issues -->

一些已知問題包括：

* **中繼資料結構**:資產評級介面工具集可能導致JSP編譯錯誤。 因應措施是從中繼資料結構中移除資產評級元件。 <!-- CQ-4282865 -->

Assets功能的一些限制包括：

* 當AEM 6.5網站部署在AMS上時，AEM Assets即為雲端服務，Connected Assets功能即可運作。

### 近期資產功能 {#upcoming-assets-capabilities}

Adobe Experience Manager Assets的一些功能依賴於基礎功能，這些功能尚未在Experience manager中作為雲端服務部署架構提供，預計將在稍後階段啟用：

* 發佈至品牌入口網站目前未啟用。 您可以擴充和部署 [資產共用共用實作](https://adobe-marketing-cloud.github.io/asset-share-commons/) ，以便進行資產散發使用案例。
* 目前不提供運用Adobe I/O AI服務的增強智慧標籤功能。
* 由於依賴Commerce Integration Framework API，此階段未啟用功能：
   * 像片拍攝工作流程模型。
   * 資產屬性使用者介面中的產品資訊標籤不會填入。
* 由於依賴InDesign server整合，目前尚未啟用功能：
   * 資產範本和資產目錄。
   * InDesign檔案的多頁預覽。

>[!MORELIKETHIS]
>
>* [AEM的主要變更](aem-cloud-changes.md)
>* [已過時和移除的功能](deprecated-removed-features.md)
>* [發行說明](home.md)

