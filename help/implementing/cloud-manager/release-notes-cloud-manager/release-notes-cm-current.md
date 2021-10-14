---
title: AEMas a Cloud Service版2021.10.0中的Cloud Manager發行說明
description: AEMas a Cloud Service版2021.10.0中的Cloud Manager發行說明
feature: Release Information
exl-id: 42cc9cab-6e66-4976-a3b1-ecb9dbaaabf4
source-git-commit: 62e9466fdfd6d6ac63dad9a2bc19693f7dc8d098
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud Service 2021.10.0中的Cloud Manager發行說明 {#release-notes}

本頁概述AEM 2021.10.0中Cloud Manager的發行說明。

>[!NOTE]
>若要查看最新的Adobe Experience Manager as a Cloud Service發行說明，請按一下[here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

AEMas a Cloud Service的Cloud Manager發行日期為2021.10.0年10月14日。
下一版預計於2021年11月4日發行。

### 新增功能 {#what-is-new}

* 為了準備一些即將進行的更改，現在將在用戶介面中引用現有部署管道，並將其標籤為&#x200B;**完整堆棧**&#x200B;管道。

* 管道卡已重新整理，現在會顯示顯示生產管道和非生產管道的單一整合面板，且使用者可從與每個管道相關聯的動作功能表中直接選取「執行/暫停/繼續」。

* 部署管理員角色中的使用者現在可以透過UI以自助方式刪除生產管道。

* 新增和編輯管道體驗已重新整理，現在可使用熟悉的現代模組。

* Cloud Manager的使用者現在可以透過登錄頁面右上角的&#x200B;**Feedback**&#x200B;按鈕，直接從使用者介面提交意見。

* 每年的SLA圖表現在可以從Cloud Manager的使用者介面下載。

* 程式碼品質和非生產管道執行現在會在建置步驟期間使用更有效率的淺層復製程式，為擁有特別大型Git存放庫的客戶提供更快的建置時間。

* 「新增IP允許清單」精靈現在會通知使用者已達到允許的IP允許清單數目上限。

* Cloud Manager API檔案現在包含互動式操作場，可讓登入的使用者透過瀏覽器試驗API。 如需詳細資訊，請參閱[Cloud Manager API Plearty](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 。

* 如果禁用「導航到」下的選擇選項，則「程式」卡上的工具提示將更具描述性。 現在會顯示「生產環境不存在」。

### 錯誤修正 {#bug-fixes}

* 在極少數情況下，當Adobe員工恢復客戶的環境時，在環境完全運行之前，會將恢復視為已完成。

* 環境建立期間提出的某些內部請求未重試。

