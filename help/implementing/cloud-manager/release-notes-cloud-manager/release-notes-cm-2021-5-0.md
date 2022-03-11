---
title: Cloud Manager在as a Cloud Service版AEM2021.5.0中的發行說明
description: Cloud Manager在as a Cloud Service版AEM2021.5.0中的發行說明
feature: Release Information
exl-id: 8ae3cf2f-1865-427a-b612-bdf56e2f0304
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2021.5.0 {#release-notes}

本頁概述了as a Cloud Service2021.5.0中Cloud Manager的發行說明AEM。

>[!NOTE]
>要查看Adobe Experience Manager as a Cloud Service的當前發行說明，請按一下 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service2021.5.0中的發佈日AEM期為2021年5月6日。

### 新增功能 {#what-is-new}

* PackageOveraps質量規則現在可檢測在同一部署的軟體包集中多次部署同一軟體包的情況，即在多個嵌入位置中。

* Public API中的儲存庫終結點現在包括Git URL。

* 雲管理器用戶下載的部署日誌將更有洞察力，現在將包括有關失敗和成功方案的詳細資訊。

* 將代碼推送到AdobeGit時遇到的間歇性故障現已解決。

* 現在，在「編輯」程式工作流期間，Commerce載入項可以應用於沙盒程式。

* 的 *編輯程式* 體驗已刷新。

* 「環境詳細資訊」(Environment Details)頁面中的「域名」(Domain Names)表格將通過分頁顯示多達250個域名。

* 的 **解決方案和附加模組** 頁籤 **添加程式** 和 **編輯程式** 工作流將顯示該解決方案，即使只有一個解決方案可用於該程式。

* 生成步驟日誌中未生成任何已部署的內容包時的錯誤消息不明確。

### 錯誤修正 {#bug-fixes}

* 有時，即使未部署IP允許清單，用戶也可能看到該配置旁邊的綠色「活動」狀態。

* 管道變數API將僅將其標籤為狀態，而不是刪除「已刪除」變數 **已刪除**。

* 某些代碼氣味類型的質量問題錯誤地影響了可靠性評級。

* 由於不支援通配符域，因此UI將不允許用戶提交通配符域。

* 在午夜到UTC凌晨1點之間開始管道執行時，Cloud Manager生成的項目版本不保證大於前一天建立的版本。

* 在沙盒程式設定期間，一旦成功建立了包含示例代碼的項目，「管理Git」將作為「概述」頁中英雄卡的連結顯示。
