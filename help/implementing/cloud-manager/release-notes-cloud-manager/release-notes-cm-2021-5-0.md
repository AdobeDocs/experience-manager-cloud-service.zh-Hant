---
title: AEM as a Cloud Service 版本 2021.5.0 中 Cloud Manager 的發行說明
description: AEM as a Cloud Service 版本 2021.5.0 中 Cloud Manager 的發行說明
feature: Release Information
exl-id: 8ae3cf2f-1865-427a-b612-bdf56e2f0304
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: ht
source-wordcount: '377'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 2021.5.0 中 Cloud Manager 的發行說明 {#release-notes}

本頁面總覽 AEM as a Cloud Service 2021.5.0 中 Cloud Manager 的發行說明

>[!NOTE]
>若要閱讀 Adobe Experience Manager as a Cloud Service 的目前發行說明，請按一下[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

AEM as a Cloud Service 2021.5.0 中的 Cloud Manager 發行日期是 2021 年 5 月 06 日。

### 新增功能 {#what-is-new}

* PackageOverlaps 品質規則現在會偵測多次部署了相同套件的情況；也就是在同一個部署的套件組中的多個嵌入式位置。

* 公用 API 中的存放庫端點現在包含 Git URL。

* Cloud Manager 使用者下載的部署記錄有更深刻的見解，而且現在包含有關失敗和成功情境的細節。

* 將計劃碼推送到 Adobe Git 時所發生的間歇性失敗狀況現在已經解決了。

* Commerce 附加元件現在可以在編輯計劃工作流程中套用到沙箱計劃。

* *編輯計劃*&#x200B;體驗已更新。

* 「環境詳細資訊」頁面中的「網域名稱」表格可透過分頁顯示多達 250 個網域名稱。

* **「新增計劃」**&#x200B;和&#x200B;**「編輯計劃」**&#x200B;工作流程中的&#x200B;**「解決方案和附加元件」**&#x200B;索引標籤會顯示解決方案，即便該計劃只有一個解決方案可用。

* 當建置未產生任何已部署的內容套件時，建置步驟記錄中的錯誤訊息不清楚。

### 錯誤修正 {#bug-fixes}

* 有時，即使未部署該設定，使用者也可能會在 IP 允許清單旁邊看到綠色的「活動」狀態。

* 管道變數 API 不會移除「已刪除」的變數，而是只會用狀態將其標記為&#x200B;**已刪除**。

* 部分計劃碼異味類型的品質問題錯誤地影響了可靠性評等。

* 由於不支援萬用字元網域，UI 將不允許使用者提交萬用字元網域。

* 在 UTC 午夜和凌晨 1 點之間開始執行管道時，不能保證 Cloud Manager 產生的成品版本大於前一天建立的版本。

* 在沙箱計畫設定過程中，成功建立包含範例計劃碼的專案後，管理 Git 將顯示為總覽頁面中英雄卡的連結。
