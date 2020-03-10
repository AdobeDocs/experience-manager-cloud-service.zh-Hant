---
title: 已知問題
description: Adobe Experience Manager 雲端服務已知問題的發行說明
translation-type: ht
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# 已知問題 {#known-issues}

本文說明 Adobe Experience Manager 雲端服務產品的已知問題。此清單會隨著 Experience Manager 推出各個版本而持續修訂和更新。

如需已知問題的詳細資訊，請[連絡支援團隊](https://helpx.adobe.com/tw/support/experience-manager.html)。

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## 資產 {#assets}

<!-- Jira label: assets-cloud-known-issues -->

部分已知問題包括：

* **中繼資料結構**：資產評等工具集可能造成 JSP 編譯錯誤。因應辦法是從中繼資料結構中移除資產評等元件。<!-- CQ-4282865 -->

Assets 功能的部分限制包括：

* 有了 AEM Assets 雲端服務，只要 AEM 6.5 Sites 部署於 AMS，連線資產的功能即可運作。

### 即將推出的 Assets 功能 {#upcoming-assets-capabilities}

Adobe Experience Manager Assets 的少數功能需仰賴基礎功能，這些基礎功能尚無法在 Experience Manager 雲端服務部署架構中使用，預計之後會啟用：

* 目前未啟用發佈至 Brand Portal 的功能。您可以為資產散佈使用案例擴充及部署 [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) 實作。
* 目前尚不提供運用 Adobe I/O AI 服務的增強智慧型標記功能。
* 目前仍仰賴 Commerce Integration Framework API 而未啟用的功能：
   * 拍攝工作流程模型。
   * 資產屬性使用者介面中未填入資料的產品資訊標籤。
* 目前仍仰賴 InDesign Server 整合而尚未啟用的功能：
   * 資產範本和資產目錄。
   * InDesign 檔案的多頁預覽。

>[!MORELIKETHIS]
>
>* [AEM 重大變更](aem-cloud-changes.md)
>* [過時和移除的功能](deprecated-removed-features.md)
>* [發行說明](home.md)

