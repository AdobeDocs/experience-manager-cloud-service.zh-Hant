---
title: 使用者對應和主體移轉
description: AEMas a Cloud Service中的使用者對應和主體移轉概觀。
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 5%

---

# 使用者對應和主體移轉 {#user-mapping-and-principal-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermapping"
>title="使用者移轉"
>abstract="內容轉移工具可協助您將使用者和群組從現有的 Adobe Experience Manager (AEM) 系統移至 AEM as a Cloud Service。必須對應現有使用者，以便他們可以透過其 IMS ID 登入。"

>[!NOTE]
>如需舊版的使用者對應工具，請參閱 [舊版檔案](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md).

## 簡介 {#introduction}

在轉換至Adobe Experience Manager (AEM)as a Cloud Service的過程中，使用者和群組（或「主體」）必須從現有的AEM系統移轉至AEMas a Cloud Service。 此工作由「內容轉移工具」完成。

AEMas a Cloud Service的重大變更是完全整合式使用AdobeID來存取製作階層。 此程式需要使用 [Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 用於管理使用者和使用者群組。 使用者設定檔資訊會集中在AdobeIdentity Management系統(IMS)中，可提供所有Adobe雲端應用程式的單一登入。 如需詳細資訊，請參閱 [Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management). 由於此變更，現有使用者必須對應至其IMS ID，才能使用其IMS設定檔存取AEMaaCS。 由於傳統AEM中的群組與IMS中的群組完全不同，群組不會相對應，但在移轉完成後必須協調兩組群組。

## 主體移轉詳細資料 {#principal-migration-detail}

內容轉移工具和Cloud Acceleration Manager會將與正在移轉的內容相關聯的任何主體移轉至雲端系統。 「內容轉移工具」會在擷取程式期間，從來源AEM系統複製所有主體，以達成此目的。 CAM擷取接著只會選取和移轉與正在擷取的內容相關聯的主參與者。 如果主體位於已移轉內容的ACL或CUG原則上，則該主體及其所在的所有群組，以及其上階（父）群組都會被移轉。 此外，如果內容上的主參與者是群組，則其所有下階（子項）群組和使用者也會移轉。

## 使用者對應詳細資訊 {#user-mapping-detail}

AEM使用者可以對應至具有相同電子郵件地址的對應Adobe IMS使用者。 此對應可以在CTT中自動完成（在擷取步驟期間），並且可以在開始擷取之前透過切換來控制它是否完成。 使用者在開始擷取時，可以覆寫切換的預設設定。

* 如果來源系統是一個作者例項，則依照預設，進行對應的選擇為 _於_，因為這是建議的流程。
* 如果來源系統是發佈執行個體，則預設情況下執行對應的選擇為 _關閉_，因為使用者通常不會移轉或用於發佈執行個體；或者如果使用這些使用者，則通常會為其使用不同的驗證系統（即非IMS）。

無論使用者在擷取期間是否進行對應，如果使用者與要移轉的內容相關聯，則會在擷取期間連同群組一起移轉至雲端系統。

## 對應和移轉使用者的重要注意事項 {#important-considerations}

### 例外情況 {#exceptional-cases}

會記錄下列特定案例：

1. 如果使用者在電子郵件中沒有電子郵件地址 `profile/email` 的欄位 *jcr* 節點，有問題的使用者可能已移轉，但未對應。 即使使用電子郵件地址作為使用者名稱登入，也會發生這種情況。
2. 如果使用者遭停用，則會與其他使用者受到相同對待；其會正常對應和移轉，並在雲端例項上維持停用狀態。
3. 如果來源AEM例項和目標AEM Cloud Service例項上的主參與者具有任何相同的唯一性限制資料（rep：principalName、rep：authorizableId、jcr：uuid或rep：externalId），則有問題的主參與者不會移轉，而雲端系統上先前存在的主參與者保持不變。 這會記錄在「主要移轉報表」中。
4. 如果使用者未透過使用者對應對應對應到IMS，則IMS將無法識別雲端AEM系統上的使用者設定檔；在此情況下，如果他們透過IMS登入，將在AEM上建立新的（重複）設定檔，但不會包含他們之前的設定檔資訊。 原始使用者設定檔將存在於雲端AEM系統中，但他們將無法透過IMS登入，僅使用傳統AEM方法（本機登入）。 因此，強烈建議對所有作者移轉對應所有使用者。

## 其他考量事項 {#additional-considerations}

* 如果設定 **在內嵌之前擦除雲端例項上的現有內容** 設定，先前轉移至Cloud Service執行個體的主體會與整個現有存放庫一併刪除；會建立新存放庫，並內嵌內容。 此程式也會重設所有設定，包括目標Cloud Service執行個體的許可權，適用於新增至的管理員使用者。 **管理員** 群組。 必須將管理員使用者重新新增至 **管理員** 群組以擷取CTT/CAM擷取的存取權杖。
* 執行非擦去內嵌時(**清除現有內容** 取消設定)，如果內容未傳輸，因為在上次傳輸後內容未變更，與該內容相關聯的使用者和群組也不會傳輸。 即使來源系統上的使用者和群組已變更，此規則仍為真。 這是因為使用者和群組只會隨著相關聯的內容一起移轉。 因此，來源系統上任何新加入群組的主參與者將不會移轉，除非他們屬於正在移轉的不同群組，或位於正在移轉的不同內容的ACL中。 若要後續移轉這些主體，請考慮使用套件，或從目標中刪除主體，然後重新移轉相關內容（以覆寫擷取並以擦去擷取）。
* IMS不允許使用重複的電子郵件地址，但在AEM中允許使用（內部部署和雲端）。 使用者可以使用他們的電子郵件地址透過IMS登入AEM，他們將會登入IMS參考的使用者設定檔。
* 另請參閱 [移轉封閉式使用者群組](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md) 封閉使用者群組(CUG)原則中所使用主體的其他考量事項。

## 最終摘要與報告 {#final-report}

擷取和內嵌成功完成後，就會產生一份報表，顯示主要移轉詳細資訊。 另請參閱 [如何驗證主體移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-principal-migration) 以取得詳細資訊。
