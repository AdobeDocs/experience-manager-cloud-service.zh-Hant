---
title: 使用者對應工具的重要考量（舊版）
description: 使用者對應工具的重要考量（舊版）
exl-id: 0d39a5be-93e1-4b00-ac92-c2593c02b740
hide: true
hidefromtoc: true
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# 使用者對應工具的重要考量（舊版） {#important-considerations}

>[!INFO]
>
>本檔案旨在說明該工具的已棄用版本。 如需最新版本的詳細資訊，請參閱 [使用者對應和主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/user-mapping-and-migration.md).

## 例外情況 {#exceptional-cases}

會記錄下列特定案例：

1. 如果使用者在電子郵件中沒有電子郵件地址 `profile/email` 的欄位 *jcr* 節點，相關使用者或群組已移轉但未對應。 即使使用電子郵件地址作為使用者名稱登入，此規則仍適用。

1. 如果在AdobeIdentity Management系統(IMS)系統上找不到所使用組織ID的電子郵件（或如果無法擷取IMS ID），則使用者或群組會移轉，但不會進行對應。

1. 如果使用者已停用，則會被視為與未停用時相同。 它會正常對應和移轉，並在雲端例項上維持停用。

1. 如果使用者存在於目標AEM Cloud Service執行個體上，且具有與來源AEM執行個體上使用者相同的使用者名稱(rep：principalName)，則不會移轉該使用者或群組。

1. 如果移轉使用者時未先透過使用者對應進行對應，則他們在目標雲端系統上將無法使用其IMS ID登入。 他們或許可以使用傳統AEM方法登入，但此工作流程通常不是所需或期望的。

## 其他考量 {#additional-considerations}

* 如果設定 **在內嵌之前擦除雲端例項上的現有內容** 設定，則會刪除Cloud Service執行個體上已轉移的使用者。 也會刪除整個現有存放庫，並建立新存放庫，在其中擷取內容。 此動作也會重設所有設定，包括目標Cloud Service執行個體的許可權，若管理員使用者新增至 **管理員** 群組。 管理員使用者必須重新導覽至 **管理員** 群組以擷取CTT的存取權杖。

* Adobe建議您在透過使用者對應執行CTT之前，從目標Cloud ServiceAEM執行個體中移除任何現有使用者。 此動作是必要的，以防止將使用者從來源AEM例項移轉至目標AEM例項之間發生任何衝突。 如果來源AEM例項和目標AEM例項中存在相同的使用者，擷取期間可能會發生衝突。

* 執行內容追加時，如果內容由於在上次轉移後未變更而未轉移，則與該內容相關聯的使用者和群組也不會轉移。 即使使用者與群組在此期間已變更，此規則仍為真。 原因是使用者和群組會隨著相關聯的內容一起移轉。

* 如果AEM Cloud Service中的使用者與來源AEM例項上的使用者具有不同使用者名稱，但電子郵件地址相同，並且已啟用「使用者對應」，則會記錄一則錯誤訊息。 此外，不會轉移來源AEM使用者，因為目標系統上只允許一位擁有指定電子郵件地址的使用者。

* 如果來源AEM執行個體上的兩個使用者擁有相同的電子郵件地址，並且已啟用「使用者對應」，則會記錄一則錯誤訊息。 此外，其中一位來源AEM使用者已轉移，因為目標系統上只允許一位具有指定電子郵件地址的使用者。

### 下一步 {#whats-next}

瞭解重要考量事項和特殊案例後，您就可以開始使用此工具了。 另請參閱 [使用使用者對應工具](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/using-user-mapping-tool-legacy.md) 以取得更多詳細資料。
