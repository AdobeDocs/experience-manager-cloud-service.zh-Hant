---
title: Cloud Manager在as a Cloud Service版AEM2021.10.0中的發行說明
description: Cloud Manager在as a Cloud Service版AEM2021.10.0中的發行說明
feature: Release Information
exl-id: f8a87b00-52ce-42a6-a955-45cb14703b40
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 3%

---

# Adobe Experience Manager as a Cloud ServiceCloud Manager發行說明2021.10.0 {#release-notes}

本頁概述了as a Cloud Service2021.10.0中Cloud Manager的發行說明AEM。

>[!NOTE]
>要查看Adobe Experience Manager as a Cloud Service的當前發行說明，請按一下 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=zh-Hant)。

## 發行日期 {#release-date}

Cloud Manager在as a Cloud Service中的AEM發佈日期為2021年10月14日。


### 新增功能 {#what-is-new}

* 為準備即將進行的一些更改，現在將在用戶介面中引用現有部署管道並將其標籤為 **完整堆棧** 管線。

* 管道卡已刷新，現在將顯示一個顯示生產管線和非生產管線的單個整合面，用戶可以直接從與每個管線關聯的操作菜單中選擇「運行/暫停/恢復」。

* 部署管理器角色中的用戶現在可以通過UI以自助方式刪除生產管道。

* 添加和編輯管道體驗已刷新，現在可使用熟悉的現代模型。

* Cloud Manager的用戶現在可以通過以下方式直接從用戶介面提交反饋： **反饋** 按鈕。

* 現在，可以從Cloud Manager的用戶介面下載年度SLA圖表。

* 代碼質量和非生產流水線執行現在將在生成步驟期間使用一個更高效的淺層克隆過程，從而為具有特別大的Git儲存庫的客戶帶來更快的生成時間。

* 「添加IP允許清單」嚮導現在將通知用戶是否已達到允許的IP允許清單的最大數量。

* Cloud Manager API文檔現在包括一個互動式操場，允許登錄用戶從其瀏覽器中試用API。 請參閱 [Cloud Manager API遊樂場](https://www.adobe.io/experience-cloud/cloud-manager/reference/playground/) 的子菜單。

* 如果禁用「導航至」下的選擇選項，則程式卡上的工具提示將更具說明性。 現在顯示「生產環境不存在」。

### 錯誤修正 {#bug-fixes}

* 在極少數情況下，當Adobe員工恢復客戶的環境時，在環境完全正常運行之前，會認為恢復已完成。

* 未重試在建立環境期間發出的某些內部請求。

* 如果在域名驗證後出現部署失敗錯誤，則已更正錯誤消息以請求客戶聯繫其Adobe代表。
