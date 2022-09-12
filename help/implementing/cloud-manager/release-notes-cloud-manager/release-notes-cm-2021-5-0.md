---
title: AEM as a Cloud Service2021.5.0版中Cloud Manager發行說明
description: AEM as a Cloud Service2021.5.0版中Cloud Manager發行說明
feature: Release Information
exl-id: 8ae3cf2f-1865-427a-b612-bdf56e2f0304
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud Service 2021.5.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM 2021.5.0as a Cloud Service版中Cloud Manager的發行說明。

>[!NOTE]
>若要查看最新的Adobe Experience Manager as a Cloud Service發行說明，請按一下 [此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html).

## 發行日期 {#release-date}

AEM 2021.5.0中的Cloud Manageras a Cloud Service日期為2021年5月6日。

### 新增功能 {#what-is-new}

* PackageOverlaps質量規則現在會檢測在同一部署的包集中多次部署相同包的情況，即在多個嵌入位置中。

* 公用API中的存放庫端點現在包含Git URL。

* Cloud Manager使用者下載的部署記錄將更有洞察力，現在會包含有關失敗和成功案例的詳細資訊。

* 現在已解決將程式碼推送至AdobeGit時發生的間歇性故障。

* 現在，在編輯方案工作流程期間，商務附加元件可套用至沙箱方案。

* 此 *編輯程式* 體驗已重新整理。

* 「環境詳細資料」頁面中的「網域名稱」表格會透過分頁顯示最多250個網域名稱。

* 此 **解決方案和附加元件** 標籤 **添加程式** 和 **編輯方案** 即使方案只有一個解決方案可用，工作流程仍會顯示解決方案。

* 當組建未產生任何已部署的內容套件時，建置步驟記錄中的錯誤訊息不清楚。

### 錯誤修正 {#bug-fixes}

* 有時，即使未部署該設定，使用者仍可能在IP允許清單旁看到綠色的「作用中」狀態。

* 管道變數API不會移除「已刪除」的變數，而只會將其標示為狀態 **已刪除**.

* 某些代碼氣味類型的質量問題錯誤地影響了可靠性等級。

* 由於不支援萬用字元網域，因此UI將不允許使用者提交萬用字元網域。

* 當午夜至凌晨1:00之間開始執行管道時，Cloud Manager產生的工件版本不一定會大於前一天建立的版本。

* 在沙箱方案設定期間，成功建立包含范常式式碼的專案後，「管理Git」會顯示為「概述」頁面中主圖卡的連結。
