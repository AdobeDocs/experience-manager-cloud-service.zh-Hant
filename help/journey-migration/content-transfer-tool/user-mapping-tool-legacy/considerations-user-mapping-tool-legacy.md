---
title: 使用者對應工具的重要考量（舊版）
description: 使用者對應工具的重要考量（舊版）
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
hide: true
hidefromtoc: true
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# 使用者對應工具的重要考量（舊版） {#important-considerations}

>[!INFO]
>
>本檔案旨在說明該工具的已棄用版本。 如需最新版本的詳細資訊，請參閱 [使用者對應和主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

## 例外情況 {#exceptional-cases}

會記錄下列特定案例：

1. 如果使用者在電子郵件中沒有電子郵件地址 `profile/email` 的欄位 *jcr* 節點，相關使用者或群組已移轉但未對應。  即使使用電子郵件地址作為使用者名稱登入，此規則仍適用。

1. 如果在AdobeIdentity Management系統(IMS)系統上找不到所使用組織ID的指定電子郵件（或由於其他原因無法擷取IMS ID），則有問題的使用者或群組會移轉但未對應。

1. 如果使用者目前為停用，則會被視為與未停用時相同。 它會正常對應和移轉，並在雲端例項上維持停用。

1. 如果使用者存在於目標AEM Cloud Service執行個體上，且具有與來源AEM執行個體上使用者相同的使用者名稱(rep：principalName)，則不會移轉有問題的使用者或群組。

1. 如果移轉使用者時未先透過使用者對應進行對應，則他們在目標雲端系統上將無法使用其IMS ID登入。  他們或許可以使用傳統AEM方法登入，但請記住，這通常不是所需或期望的。

## 其他考量 {#additional-considerations}

* 如果設定 **在內嵌之前擦除雲端例項上的現有內容** 設定，則會刪除Cloud Service執行個體上已轉移的使用者以及整個現有存放庫，並建立一個新存放庫以將內容擷取到。 這也會重設所有設定，包括目標Cloud Service執行個體的許可權，新增至的管理員使用者則為true **管理員** 群組。 管理員使用者需要重新新增至 **管理員** 群組以擷取CTT的存取權杖。

* 建議先從目標Cloud ServiceAEM執行個體中移除任何現有使用者，然後再使用使用者對應執行CTT。 這是為了避免將使用者從來源AEM例項移轉至目標AEM例項時發生任何衝突。 如果來源AEM例項和目標AEM例項中存在相同的使用者，則在擷取期間將會發生衝突。

* 執行內容追加時，如果內容由於自上次轉移以來未變更而未轉移，則與該內容相關聯的使用者和群組也不會轉移，即使使用者和群組在此期間已變更。 這是因為使用者和群組會隨著相關聯的內容一起移轉。

* 如果目標AEM Cloud Service執行個體中的使用者與來源AEM執行個體上的其中一位使用者具有不同的使用者名稱，但電子郵件地址相同，並且已啟用「使用者對應」，則會在記錄中寫入錯誤訊息，且不會傳輸來源AEM使用者，因為目標系統上只允許一位具有指定電子郵件地址的使用者。

* 如果來源AEM執行個體上的兩個使用者擁有相同的電子郵件地址，並且已啟用「使用者對應」，則會在記錄中寫入錯誤訊息，並且不會傳輸其中一個來源AEM使用者，因為目標系統上僅允許具有給定電子郵件地址的一名使用者。

### 下一步 {#whats-next}

瞭解重要考量事項和特殊案例後，您就可以開始使用此工具了。 另請參閱 [使用使用者對應工具](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/using-user-mapping-tool-legacy.md) 以取得更多詳細資料。
