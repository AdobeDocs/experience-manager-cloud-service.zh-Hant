---
title: AEM as aCloud Service中Cloud Manager的發行說明2020.6.0版
description: AEM as aCloud Service中Cloud Manager的發行說明2020.6.0版
feature: 發行資訊
exl-id: 879a5025-f94f-4549-bf6e-e1cc6b6a7b58
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 83%

---

# Adobe Experience Manager as aCloud Service2020.6.0 {#release-notes}中的Cloud Manager發行說明

本頁概述AEM as a 2020.6.0Cloud Service中Cloud Manager的發行說明。

## 發行日期 {#release-date}

AEM as aCloud Service2020.6.0中的Cloud Manager發行日期為2020年6月4日。

## 新功能 {#whats-new-cloud-manager}

* 在 Cloud Manager 中，屬於&#x200B;*業務擁有者*&#x200B;角色的使用者現在可以從登陸頁面 (透過「方案」卡片上的快速動作按鈕) 或從方案中刪除沙箱方案。

   如需詳細資訊，請參閱[刪除沙箱方案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html)。

* 在 Cloud Manager 中，屬於&#x200B;*業務擁有者*&#x200B;或&#x200B;*部署管理員*&#x200B;角色的沙箱方案使用者現在可以刪除透過 Cloud Manager UI 設定的生產和預備環境。現在，您可以從&#x200B;**方案概覽**&#x200B;頁面和&#x200B;**環境**&#x200B;頁面上的「環境」卡片中使用刪除選項。在「生產」或「預備」上選取刪除選項，也可刪除集合中的其他項目。

   如需詳細資訊，請參閱[刪除沙箱方案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html)。

* 登陸頁面上的「指導」標記可為使用者提供關於基本導覽的通知和指示。

* **方案概覽**&#x200B;頁面上的「指導」標記，可為使用者提供與 Cloud Manager 中的基本導覽有關的通知和指示，方便他們開始使用。

* 現在，Cloud Manager 中提供&#x200B;**學習**&#x200B;頁面，可透過上層導覽存取。此頁面提供相關資源，可協助使用者了解與他們在 Cloud Manager 中指派的角色有關的常用工作流程。

* 「沙箱方案」現在可透過&#x200B;**沙箱**&#x200B;徽章來識別，此徽章會顯示在登陸頁面的方案卡片上，以及&#x200B;**方案概覽**&#x200B;頁面中的方案名稱旁。

* 現在，SysAdmin 角色中的使用者可以從可管理 Cloud Manager 使用者角色或權限的位置，單鍵存取 Admin Console 中的位置。在登陸頁面上，**新增方案**&#x200B;按鈕旁現在有&#x200B;**管理存取**&#x200B;按鈕可供使用。

   如需詳細資訊，請參閱 [SysAdmin 任務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks)。

* SysAdmin 角色中的使用者現在可以直接從 Cloud Manager 單鍵存取製作例項。

   如需詳細資訊，請參閱[管理對製作例項的存取](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem)。

* 「建置」記錄現在包含探索到的成品清單，包括略過的內容封裝。

* 「建置」步驟現在會驗證所有產生的內容封裝皆包含所有必要屬性 - 名稱、群組和版本。

* 「建置」步驟現在會驗證組建是否至少產生了一個內容封裝。

### 錯誤修正 {#bug-fixes-cm}

* 在某些情況下，**建立方案**&#x200B;對話方塊中的圖示不會對齊。

* AEM 版本識別碼不一定會顯示在&#x200B;**方案概覽**&#x200B;頁面上。

* 在設定生產管道時，某些客戶看不到&#x200B;**排定的部署**&#x200B;選項。

### 已知問題 {#known-issues-cm}

* 在特定期間內未偵測到任何活動時，沙箱方案中的環境將會休眠。在 Cloud Manager 中不會觀察到此狀態。不過，您可透過開發人員控制台來觀察此狀態。此問題將在即將發行的版本中解決。

* 直接從 Cloud Manager 連結至開發人員控制台時，不會顯示將沙箱方案的環境解除休眠/休眠的選項。若要解決此問題，請於開發人員控制台中，在 URL 的結尾處加上 `#release-cm-p1234-e5678` 模式，其中，*1234* 是方案 ID，*5678* 是環境 ID。此問題將在即將發行的版本中解決。
