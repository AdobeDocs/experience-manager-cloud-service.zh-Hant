---
title: 用戶映射工具的重要注意事項
description: 用戶映射工具的重要注意事項
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 用戶映射工具的重要注意事項 {#important-considerations}


## 特殊案件 {#exceptional-cases}

將記錄以下特定案例：

1. 如果用戶在 `profile/email` 他們 *jcr* 節點將遷移或未映射有關的用戶或組。

1. 如果在AdobeIdentity Management系統(IMS)系統上找不到使用的組織ID的給定電子郵件（或如果由於其他原因無法檢索IMS ID），則將遷移有關的用戶或組，但不映射。

1. 如果用戶當前被禁用，則其處理方式與未禁用時相同。 它將照常被映射和遷移，並將在雲實例上保持禁用狀態。

1. 如果目標AEM Cloud Service實例上存在與源實例上的用戶之一具有相同用戶名(rep:principalName)的用戶AEM，則不遷移該用戶或組。

## 其他注意事項 {#additional-considerations}

* 如果設定 **在接收之前擦除雲實例上的現有內容** 設定，Cloud Service實例上已傳輸的用戶將與整個現有儲存庫一起刪除，並將建立新儲存庫以將內容插入。 這還會重置所有設定，包括對目標Cloud Service實例的權限，對於添加到 **管理員** 組。 需要將管理員用戶重新添加到 **管理員** 組以檢索CTT的訪問令牌。

* 建議在運行帶用戶映射的CTT之前，從目AEM標Cloud Service實例中刪除任何現有用戶。 這是為了防止將用戶從源實例遷移到目AEM標實例之間發AEM生衝突。 如果源實例和目標實例上存在同一用戶，則在AEM接收過程中將發AEM生衝突。

* 執行內容補充時，如果內容自上次傳輸後未發生更改而未傳輸，則與該內容關聯的用戶和組也不會傳輸，即使與此同時用戶和組發生了更改。 這是因為用戶和組與其關聯的內容一起遷移。

* 如果目標AEM Cloud Service實例具有與源實例上的某個用戶具有相同用戶名但電子郵件地址的用戶AEM，並且啟用了「用戶映射」，則將在日誌中寫入錯誤消息，並且源用戶不會被傳輸，因為目標系統上只允許一個具有給定電子郵件地址的用戶。

* 如果源實例上的兩個AEM用戶具有相同的電子郵件地址，並且啟用了「用戶映射」，則將在日誌中寫入錯誤消息，並且不會傳輸源用戶中的一個，因為目標系統上只允許一個具有給定電子郵件地址的用戶AEM。

### 下一步是什麼 {#whats-next}

一旦您瞭解了重要注意事項和特殊情況，您現在就可以使用該工具。 請參閱 [使用用戶映射工具](/help/journey-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.md) 的子菜單。
