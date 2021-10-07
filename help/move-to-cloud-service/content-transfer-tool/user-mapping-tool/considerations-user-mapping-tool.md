---
title: 使用者對應工具的重要考量
description: 使用者對應工具的重要考量
source-git-commit: 60e67e92f4f1ecaaf12c58f16f4324868d223934
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---


# 使用者對應工具的重要考量 {#important-considerations}


## 例外案例 {#exceptional-cases}

將記錄下列特定案例：

1. 如果使用者的&#x200B;*jcr*&#x200B;節點的`profile/email`欄位中沒有電子郵件地址，則有關的使用者或群組將會移轉，但不會對應。

1. 如果在AdobeIdentity Management系統(IMS)系統上找不到所使用組織ID的指定電子郵件（或如果IMS ID因其他原因無法擷取），則相關的使用者或群組將會移轉，但不會對應。

1. 如果用戶當前已禁用，則會將其視為與未禁用相同。 它會照常對應和移轉，並在雲端例項上保持停用狀態。

1. 如果目標AEM Cloud Service實例上存在與源AEM實例上的某個用戶同名的用戶(rep:principalName)，則不會遷移該用戶或組。

## 其他考量事項 {#additional-considerations}

* 如果設定「在擷取&#x200B;**之前擦去雲端例項上的現有內容」 ，則Cloud Service例項上已轉移的使用者將會與整個現有存放庫一起刪除，並會建立新存放庫以將內容擷取至。**&#x200B;這也會重設所有設定，包括目標Cloud Service例項的權限，且新增至&#x200B;**administrators**&#x200B;群組的管理員使用者為true。 管理員使用者需要重新新增至&#x200B;**administrators**&#x200B;群組，才能擷取CTT的存取權杖。

* 建議您先從目標Cloud ServiceAEM例項移除任何現有使用者，再透過「使用者對應」執行CTT。 這是為了防止將使用者從來源AEM例項移轉至目標AEM例項之間發生任何衝突。 如果來源AEM例項和目標AEM例項上存在相同的使用者，擷取期間便會發生衝突。

* 執行內容追加時，如果自上次轉移後內容未變更而未轉移，則與該內容相關聯的使用者和群組也不會轉移，即使在此期間使用者和群組已變更亦然。 這是因為使用者和群組會與其相關聯的內容一起移轉。

* 如果目標AEM Cloud Service實例具有與源AEM實例上的某個用戶具有不同用戶名但電子郵件地址相同的用戶，並且啟用了用戶映射，則日誌中將寫入錯誤消息，並且源AEM用戶將不會被轉移，因為目標系統上只允許一個具有給定電子郵件地址的用戶。

* 如果源AEM實例上的兩個用戶具有相同的電子郵件地址，並且啟用了「用戶映射」，則日誌中將會寫入一條錯誤消息，並且不會傳輸一個源AEM用戶，因為目標系統上只允許一個具有指定電子郵件地址的用戶。

### 下一步 {#whats-next}

了解重要考量事項和特殊案例後，您現在已準備好使用此工具。 如需詳細資訊，請參閱[使用使用者對應工具](/help/move-to-cloud-service/content-transfer-tool/user-mapping-tool/using-user-mapping-tool.md) 。