---
title: AEM as aCloud Service中Cloud Manager的發行說明2021.5.0版
description: AEM as aCloud Service中Cloud Manager的發行說明2021.5.0版
feature: 發行資訊
source-git-commit: 13d45a02169fc99be60d73dde91dbc8c2ce03ef8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---


# Adobe Experience Manager as aCloud Service2021.5.0 {#release-notes}中的Cloud Manager發行說明

本頁概述AEM as a 2021.5.0Cloud Service中Cloud Manager的發行說明。

>[!NOTE]
>若要查看Adobe Experience Manager as aCloud Service的最新發行說明，請按一下[here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

AEM as aCloud Service中的Cloud Manager 2021.5.0的發行日期為2021年5月6日。
下一版預計於2021年6月10日發行。

### 新功能 {#what-is-new}

* PackageOverlaps質量規則現在會檢測在同一部署的包集中多次部署相同包的情況，即在多個嵌入位置中。

* 公用API中的存放庫端點現在包含Git URL。

* Cloud Manager使用者下載的部署記錄將更有洞察力，現在會包含有關失敗和成功案例的詳細資訊。

* 現在已解決將程式碼推送至AdobeGit時發生的間歇性故障。

* 現在，在編輯方案工作流程期間，商務附加元件可套用至沙箱方案。

* 已重新整理&#x200B;*編輯程式*&#x200B;體驗。

* 「環境詳細資料」頁面中的「網域名稱」表格會透過分頁顯示最多250個網域名稱。

* **Add Program**&#x200B;和&#x200B;**Edit Program**&#x200B;工作流程中的&#x200B;**Solutions &amp; Add-ons**&#x200B;標籤將顯示解決方案，即使該程式只有一個解決方案可用。

* 當組建未產生任何已部署的內容套件時，建置步驟記錄中的錯誤訊息不清楚。

### 錯誤修正 {#bug-fixes}

* 有時，即使未部署該設定，使用者仍可能在IP允許清單旁看到綠色的「作用中」狀態。

* 管道變數API不會移除「已刪除」變數，而只會以狀態&#x200B;**DELETED**&#x200B;來標籤它們。

* 某些代碼氣味類型的質量問題錯誤地影響了可靠性等級。

* 由於不支援萬用字元網域，因此UI將不允許使用者提交萬用字元網域。

* 當午夜至凌晨1:00之間開始執行管道時，Cloud Manager產生的工件版本不一定會大於前一天建立的版本。

* 在沙箱方案設定期間，成功建立包含范常式式碼的專案後，「管理Git」會顯示為「概述」頁面中主圖卡的連結。
