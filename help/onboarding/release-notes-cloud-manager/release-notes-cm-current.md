---
title: Cloud Manager的發行說明，作AEM為Cloud Service版本2021.5.0
description: Cloud Manager的發行說明，作AEM為Cloud Service版本2021.5.0
feature: 發行資訊
translation-type: tm+mt
source-git-commit: 29bc3d02295fb04f3aacda41c43d1733092e1f27
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---


# Adobe Experience ManagerCloud Manager的發行說明，Cloud Service2021.5.0 {#release-notes}

本頁概述了Cloud Manager的發行說明，AEM作為Cloud Service2021.5.0。

>[!NOTE]
>要將當前的Adobe Experience Manager發行說明視為Cloud Service，請按一下[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

Cloud Manager作為2021.5.0版Cloud ServiceAEM的發行日期為2021年5月6日。
下一版預計於2021年6月03日推出。

### 新功能 {#what-is-new}

* PackageOverlaps品質規則現在會偵測在相同部署的套件集中，同一套件已部署多次（即在多個內嵌位置）的情況。

* Public API中的儲存庫端點現在包含Git URL。

* 由Cloud Manager用戶下載的部署日誌將更加深入，現在將包含有關失敗和成功案例的詳細資訊。

* 現在已解決將程式碼推送至AdobeGit時間不斷發生的故障。

* 商務附加元件現在可在編輯程式工作流程中套用至沙盒程式。

* 已刷新&#x200B;*編輯程式*&#x200B;體驗。

* 「環境詳細資訊」(Environment Details)頁中的「域名」(Domain Names)表將通過分頁顯示多達250個域名。

* 在&#x200B;**Add Program**&#x200B;和&#x200B;**Edit Program**&#x200B;工作流程中，即使只有一個解決方案可供程式使用，**Solutions &amp; Add-ons**&#x200B;標籤仍會顯示解決方案。

* 當組建未產生任何已部署的內容封裝時，不清楚組建步驟記錄中的錯誤訊息。

### 錯誤修正 {#bug-fixes}

* 有時，即使未部署IP允許清單，使用者仍可能在該設定旁看到綠色的「作用中」狀態。

* 管線變數API不會移除&#39;deleted&#39;變數，而只會以狀態&#x200B;**DELETED**&#x200B;來標籤它們。

* 某些「程式碼氣味」類型的品質問題錯誤地影響「可靠性評等」。

* 由於不支援萬用字元網域，因此UI將不允許使用者提交萬用字元網域。

* 當管道執行在午夜到凌晨1點之間啟動時，Cloud Manager生成的對象版本不保證大於前一天建立的版本。

* 在沙盒程式設定期間，當已成功建立包含范常式式碼的專案後，「管理Git」就會在「概述」頁面中顯示為英雄卡的連結。