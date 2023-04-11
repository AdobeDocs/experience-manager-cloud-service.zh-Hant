---
title: 使用者對應和主體移轉
description: 使用者對應和主要移轉概觀
source-git-commit: 5475f9995513d09e61bd8f52242b3e74b8d4694c
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 11%

---

# 使用者對應和主體移轉 {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="使用者對應"
>abstract="內容轉移工具可協助您將使用者和群組從現有的 AEM 系統移至 AEM as a Cloud Service。現有使用者需要對應到他們的 IMS ID，以避免 Cloud Service 製作執行個體上出現重複的使用者。"

>[!NOTE]
>如需舊版使用者對應工具，請參閱 [舊版檔案](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## 簡介 {#introduction}

在轉換至Adobe Experience Manager(AEM)的as a Cloud Service過程中，您必須將使用者和群組從您現有的AEM系統移至AEMas a Cloud Service。 這是由「內容轉移工具」完成。

AEM as a Cloud Service 最重大的變更是完全整合使用 Adobe ID 以存取作者層。這需要使用 [Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 用於管理使用者和使用者群組。 AdobeIdentity Management系統(IMS)會集中提供使用者設定檔資訊，以針對所有Adobe雲端應用程式提供單一登入。 如需詳細資訊，請參閱 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html#identity-management). 因為此變更，現有使用者必須對應至其IMS ID，以避免Cloud Service製作例項上出現重複的使用者。 由於傳統AEM中的群組與IMS中的群組基本不同，因此群組並未對應，但移轉完成後必須調解兩組群組。

## 使用者對應和移轉詳細資訊 {#user-mapping-detail}

「內容轉移工具」和Cloud Acceleration Manager將移轉與要移轉之內容相關聯的任何使用者。 此對應會自動完成，而且可以在開始擷取之前，透過切換來控制是否完成。 開始提取時，使用者可以覆寫切換的預設設定。

* 如果來源系統是製作例項，依預設，執行對應的選項為 _on_，因為這是建議的程式。
* 如果源系統是發佈實例，預設情況下，執行映射的選擇是 _關閉_，因為使用者通常不會移轉或用於發佈執行個體。

## 對應和移轉使用者的重要注意事項 {#important-considerations}


### 例外案例 {#exceptional-cases}

記錄下列特定案例：

1. 若使用者在 `profile/email` 欄位 *jcr* 可能遷移有關用戶或組的節點，但不會映射。 即使使用電子郵件地址做為登入的使用者名稱，也會是此情況。

1. 如果用戶被禁用，則會將其視為與未禁用的一樣。 會照常對應和移轉，並在雲端例項上維持停用狀態。

1. 如果目標AEM Cloud Service例項上有與來源AEM例項上的其中一個使用者具有相同使用者名稱(rep:principalName)的使用者，則不會移轉該使用者或群組。

1. 如果使用者在移轉時未先透過「使用者對應」進行對應，或者其電子郵件地址與用來登入IMS的電子郵件地址不符，則在目標雲端系統上，他們將無法使用其IMS ID登入。 他們可能能使用傳統AEM方法登入，但請記住，這不是通常需要或預期的。


## 其他考量事項 {#additional-considerations}

* 若設定 **擷取前先擦去雲端例項上的現有內容** 已設定，則會刪除Cloud Service例項上已轉移的使用者，以及整個現有存放庫，並建立新存放庫以將內容內嵌至。 這也會重設所有設定，包括目標Cloud Service例項的權限，若管理員使用者已新增至 **管理員** 群組。 管理員使用者必須重新新增至 **管理員** 群組以擷取CTT的存取權杖。
* 當執行內容追加時，如果由於自上次轉移以來內容未更改而未轉移內容，則與該內容相關聯的用戶和組也不會轉移，即使用戶和組在此期間已發生更改。 這是因為使用者和群組會與其相關聯的內容一起移轉。
* 如果目標AEM Cloud Service實例具有與源AEM實例上的某個用戶具有不同用戶名但電子郵件地址相同的用戶，並且啟用了「用戶映射」，則日誌中會寫入錯誤消息，並且不會傳輸源AEM用戶，因為目標系統上只允許一個具有給定電子郵件地址的用戶。
