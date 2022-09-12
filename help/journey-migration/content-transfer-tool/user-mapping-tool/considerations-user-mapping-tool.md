---
title: 使用者對應工具的重要考量
description: 使用者對應工具的重要考量
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 使用者對應工具的重要考量 {#important-considerations}


## 例外案例 {#exceptional-cases}

將記錄下列特定案例：

1. 若使用者在 `profile/email` 欄位 *jcr* 節點將遷移有關用戶或組，但未映射。

1. 如果在AdobeIdentity Management系統(IMS)系統中找不到所使用組織ID的指定電子郵件（或如果IMS ID因其他原因無法擷取），則相關的使用者或群組將會移轉，但不會對應。

1. 如果用戶當前已禁用，則會將其視為與未禁用相同。 它會照常對應和移轉，並在雲端例項上保持停用狀態。

1. 如果目標AEM Cloud Service實例上存在與源AEM實例上的某個用戶同名的用戶(rep:principalName)，則不會遷移該用戶或組。

## 其他考量事項 {#additional-considerations}

* 若設定 **擷取前先擦去雲端例項上的現有內容** 已設定，則會刪除Cloud Service例項上已轉移的使用者，以及整個現有存放庫，並建立新存放庫以將內容內嵌至。 這也會重設所有設定，包括目標Cloud Service例項的權限，若管理員使用者已新增至 **管理員** 群組。 管理員使用者需要重新新增至 **管理員** 群組以擷取CTT的存取權杖。

* 建議您先從目標Cloud ServiceAEM例項移除任何現有使用者，再透過「使用者對應」執行CTT。 這是為了防止將使用者從來源AEM例項移轉至目標AEM例項之間發生任何衝突。 如果來源AEM例項和目標AEM例項上存在相同的使用者，擷取期間便會發生衝突。

* 執行內容追加時，如果自上次轉移後內容未變更而未轉移，則與該內容相關聯的使用者和群組也不會轉移，即使在此期間使用者和群組已變更亦然。 這是因為使用者和群組會與其相關聯的內容一起移轉。

* 如果目標AEM Cloud Service實例具有與源AEM實例上的某個用戶具有不同用戶名但電子郵件地址相同的用戶，並且啟用了用戶映射，則日誌中將寫入錯誤消息，並且源AEM用戶將不會被轉移，因為目標系統上只允許一個具有給定電子郵件地址的用戶。

* 如果源AEM實例上的兩個用戶具有相同的電子郵件地址，並且啟用了「用戶映射」，則日誌中將會寫入一條錯誤消息，並且不會傳輸一個源AEM用戶，因為目標系統上只允許一個具有指定電子郵件地址的用戶。

### 下一步 {#whats-next}

了解重要考量事項和特殊案例後，您現在已準備好使用此工具。 請參閱 [使用使用者對應工具](/help/journey-migration/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.md) 以取得更多詳細資訊。
