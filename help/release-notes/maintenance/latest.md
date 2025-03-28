---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本發行說明。'
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 67b9a5f73f1f8c599e902a0ac0d8efbc614c7f75
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 32%

---


# 維護版本發行說明 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本發行說明。

## 版本X {#X}

以下摘要說明維護版本X的持續改善，該版本於2025年4月1日公開發佈。 前一個維護版本是版本 19823。

啟用 2025.4.0 功能將可使用此維護版本的完整功能集。如需詳細資訊，請參閱 [Experience Manager 發行藍圖](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap)。

### 增強功能 {#enhancements-X}

Forms-19068：新增對Forms API中AEP Connector提交動作的支援，以增強表單資料整合功能。

Forms-18513：在AEP Connector中實作資料樹狀結構轉換支援，以增強精靈功能和資料處理功能。

Forms-18432：實作表單專用（規則運算式）使用者端預填設定，以啟用選擇性預填功能而無OSGI層級變更。

Forms-17551：新增SharePoint清單整合的記錄檔案(DoR)支援。

### 已修正的問題 {#fixed-issues-X}

Forms-19028：使用者端預填功能會中斷表單事件處理，導致Value commit和DOMContentLoaded事件無法在表單載入時正確觸發。

Forms-18360：在SharePoint檔案管理中增強團隊網站的Forms清單範圍管理，以改善資料組織和存取控制。

Forms-18325：新增Adobe Experience Platform (AEP)雲端設定，以增強表單資料整合與處理功能。

Forms-18213：實作功能以隱藏/排除記錄檔案(DoR)中已停用的欄位，以改善檔案清晰度和使用者體驗。

Forms-18189：修改自訂函式處理，以防止空白使用者端程式庫的錯誤記錄，並改善UI中的錯誤顯示。

Forms-18426：當清單名稱包含特殊字元（例如，「 — 」）時，SharePoint清單查詢功能會失敗，影響表單與SharePoint清單的整合。

Forms-18375：當未選取特定組態容器時，基礎元件型表單從`conf/global`資料夾中錯誤地選取recaptcha組態。

Forms-18304：在Acrobat和LiveCycle ES4中通過驗證的PDF/A-1b檔案在AEM 6.5 Forms中被錯誤地標籤為不相容，因為發生了與裝置相關的顏色錯誤。

Forms-18271： Forms主題編輯器顯示未本地化的錯誤訊息，這會影響表單設定和主題自訂的使用者體驗。

Forms-18068：使用RTF欄位的選項按鈕和核取方塊群組的記錄檔案(DoR)中出現粗體文字轉譯問題。

Forms-7016：表單編輯器中的鍵盤焦點順序未依循邏輯導覽。

Forms-6950：為檔案系統導覽器樹狀檢視元件新增必要的ARIA角色和屬性，以改進熒幕助讀程式的可存取性，並符合WCAG 4.1.2名稱、角色、值（A級）標準。

### 已知問題 {#known-issues-X}

無。

### 已過時的功能和 API {#deprecated-X}

[「已過時和已移除的功能及 API」](/help/release-notes/deprecated-removed-features.md)文件中詳細介紹 AEM as a Cloud Service 中已過時和已移除的功能及 API。

### 安全性修正 {#security-X}

AEM as a Cloud Service 專門負責將您的平台的安全性與效能最佳化。此維護發行版本解決X所發現的弱點，強化我們對強大系統保護的承諾。

### 內嵌技術 {#embedded-tech-X}

| 技術 | 版本 | 連結 |
|---|---|---|
| AEM Oak | 1.76.0 | [Oak API 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| AEM SLING API | 2.27.6 | [Apache Sling API 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.27.0 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
