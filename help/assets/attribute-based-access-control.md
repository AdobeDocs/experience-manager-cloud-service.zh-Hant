---
title: 屬性型存取控制
description: 瞭解如何啟用屬性型存取控制來定義中繼資料型規則，以定義Content Hub中可用資產的存取層級
role: Admin
badgeSaas: label="AEM Assets" type="Positive" tooltip="適用於AEM Assets)。"
exl-id: 05f54b05-40b8-4a6c-af8f-5c3f7a2089d4
source-git-commit: b736af556c8580d005097c27cceba050b21a57c9
workflow-type: tm+mt
source-wordcount: '2139'
ht-degree: 2%

---


# 屬性型存取控制 {#attribute-based-access-control}

屬性型存取控制(ABAC)可讓Content Hub管理員定義中繼資料型規則，以控制Content Hub中可用資產的存取層級。

組織的管理員會為對應至群組ID的使用者群組定義規則。 規則是[邏輯運運算元和比較運運算元](#supported-rule-constructs)的組合，管理員可視需要定義任意數量的規則，以管理Content Hub中的資產存取許可權。

規則是根據中繼資料。 如果規則中定義的條件符合資產中繼資料，則會向使用者群組顯示資產。 Content Hub會針對&#x200B;**所有Assets**&#x200B;和&#x200B;**集合**&#x200B;內可用的所有資產，掃描資產中繼資料（包括自訂中繼資料），以向使用者群組顯示結果。

例如，當資產中繼資料符合「品牌=品牌X」和「地區= EMEA或美洲」時，允許存取群組識別碼為1011的使用者群組。 Content Hub只會針對ID = 1011的使用者群組顯示資產，其中&quot;Brand = Brand X&quot;及&quot;Region = EMEA或美洲&quot;。

Content Hub中的ABAC規則可使用以下方法設定：

* **自助設定**&#x200B;使用Content Hub中的[AI助理](#configure-abac-using-ai-assistant-in-content-hub) （由AEM治理代理程式提供技術支援）
* **試算表式組態**&#x200B;透過[Adobe支援](#configure-abac-using-spreadsheet)

透過Content Hub中的AI助理，管理員可以使用中繼資料和自然語言來定義和管理ABAC規則。 這可讓您更快設定規則，並減少手動支援工作流程的相依性。

屬性式存取控制的一些主要優點包括：

* 除去對資料夾結構的權限相依性
* 讓管理員能夠上傳資產並回溯性判定權限結構
* 減少重複專案數並改善資產完整性。 當相同的資產與不同群組共用時，資料夾型許可權需要重複專案。
* 啟用細微的規則型存取
* 支援跨品牌和區域的可擴充控管
* 改善資產管理

>[!VIDEO](https://video.tv.adobe.com/v/3475413/?learn=on&enablevpops){transcript=true}

## 如何啟用以屬性為基礎的存取控制 {#enable-attribute-based-access-control}

Content Hub中的ABAC規則可使用以下方法設定：

* **使用Content Hub中的AI助理的自助設定（由AEM Governance Agent提供技術支援）**\
  管理員可以在Content Hub中使用自然語言，直接定義和管理ABAC規則。

* **透過Adobe支援的試算表式組態**\
  管理員可以在試算表中定義ABAC規則，並透過Adobe支援提交以進行設定。

## 在Content Hub中使用AI助理設定ABAC

Content Hub中的AI Assistant採用AEM Governance Agent技術，您可以使用自然語言直接在Content Hub中建立和管理ABAC規則。

您可以：
* 搜尋現有規則
* 建立規則
* 更新規則
* 刪除規則

如此一來，管理員就能建立和管理存取規則，而不需依賴支援工作流程。

### 開始之前 {#before-you-begin-ai-assistant}

在針對ABAC規則設定使用Content Hub中的AI助理之前，請確定下列事項：

* 您已獲得AEM as a Cloud Service的授權
* 由AEM Governance Agent提供支援的AI Assistant可供您的組織使用
* 如果您尚未取得存取權，請聯絡您的Adobe代表，並完成必要的授權步驟
* try-buy程式不需要GenAI附加程式

### 使用AI助理設定ABAC規則的步驟 {#steps-ai-assistant}

1. 在Content Hub中開啟AI助理。

1. 從簡單的指示開始。

   例如：

   `Create a new rule in Content Hub`

   AI Assistant會引導您瞭解建立規則所需的資訊。

1. 以自然語言定義規則。

   例如：

   `Frescopa Web Marketers user group should have access to assets where product equals Frescopa`

1. 選取必須套用ABAC規則的環境。

1. 在套用規則之前，請先檢閱規則。

   AI助理會產生規則的結構化預覽。 不會自動套用任何專案。 您可以檢閱產生的規則，視需要加以調整，或在套用之前取消動作。

1. 儲存並套用規則。

   儲存後，規則會根據中繼資料以動態方式強制執行。

此檢閱步驟有助於確保在套用規則之前的準確性。

### 使用提示管理ABAC規則 {#manage-abac-rules-using-prompts}

開始使用AI Assistant後，您可以對話式管理ABAC規則。

**探索規則**

* 顯示所有現有Content Hub ABAC規則

**建立規則**

* 建立可讓產品行銷群組存取所有資產的規則
* 讓銷售群組存取地區等於EMEA的資產

**更新規則**

* 更新EMEA行銷群組規則以包含APAC

**刪除規則**

* 刪除產品行銷群組的規則

**探索中繼資料和群組**

* 顯示可用群組和中繼資料屬性以設定規則

## 使用試算表設定ABAC

如果您的組織未啟用AI助理，您可以使用試算表式工作流程來設定ABAC規則。

按一下&#x200B;**下載試算表**，即可下載試算表中規則並加以定義。 建立Adobe支援票證，並將試算表中定義的規則提供給Adobe。

[!BADGE 下載試算表]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/ABAC_Get_Started_Template.xlsx"}

使用本文所述的准則，在試算表中定義規則。

>[!IMPORTANT]
>
>定義規則後，導覽至試算表的&#x200B;**驗證錯誤**&#x200B;標籤，然後按一下&#x200B;**執行ABAC驗證**。 已傳遞&#x200B;**所有驗證**&#x200B;訊息，確認您可以向Adobe提供定義的規則。

### 使用試算表設定ABAC規則的步驟 {#steps-spreadsheet}

1. 下載ABAC試算表範本。
1. 使用中繼資料型條件定義試算表中的規則。
1. 將每個規則對應至適當的IMS群組ID。
1. 在註解中擷取規則的商業目的。
1. 提交Adobe支援票證，並與Adobe共用完成的試算表。
1. Adobe會為貴組織設定規則。

## 以屬性為基礎的存取控制使用案例範例 {#example-metadata-based-rules}

為了支援大規模行銷推出，地區和品牌的不同團隊成員需要存取數位資產。 每個角色都有根據地區和品牌的特定範圍。 ABAC會使用資產中繼資料自動強制這些規則。 下表說明此使用案例的角色以及套用的規則：

| 人物誌 | 角色 | 角色說明 | 群組識別碼 | ABAC規則 |
|---|---|---|---|---|
| John | EMEA行銷負責人 | 監督EMEA地區所有品牌的行銷執行。 需要存取所有針對EMEA市場之品牌的已核准資產。 | 群組 — 歐洲、中東及非洲地區 — 行銷 | 地區= &quot;EMEA&quot; |
| Mike | APAC行銷負責人 | 監督APAC中所有品牌的行銷執行。 需要存取專為APAC市場設計的所有品牌的已核准資產。 | group-apac-marketing | 地區= &quot;APAC&quot; |
| Sophie | 品牌X管理員(EMEA) | 管理EMEA地區的X品牌識別。 只需要看到針對EMEA市場量身打造的Brand X核准內容。 | group-emea-brandx | 地區= &quot;EMEA&quot; &amp;&amp; brand = &quot;Brand X&quot; |
| Tom | 品牌Y管理員(APAC) | 在APAC中管理Y品牌識別。 只需要看到Brand Y核准的專為APAC市場量身打造的內容。 | group-apac-brandy | 地區= &quot;APAC&quot; &amp;&amp; brand = &quot;Brand Y&quot; |

使用這些規則，Content Hub管理員可以：

* **精細、以規則為基礎的存取**：使用者只能看到與其地區和品牌相關的資產，不需要手動指派許可權。
* **緊密的全球共同作業**：區域與品牌團隊同時運作，不會發生存取衝突。
* **可擴充且符合未來的校訂許可權**：隨著新地區或品牌的加入，可以根據中繼資料更新規則。

### ABAC有用的其他案例 {#additional-scenarios-abac}

ABAC也可以協助處理下列情況：

* **全球品牌和區域存取**：團隊只會看到與其品牌和市場相關的資產。
* **代理與合作夥伴共同作業**：外部代理與合作夥伴只能存取與其相關的行銷活動資產。
* **不同團隊的角色型存取權**：行銷、銷售和法務等團隊可以存取與其功能相關的資產。
* **特定地區法規遵循**：使用者可受限於針對特定法規或地區要求核准的資產。

>[!IMPORTANT]
>
>根據預設，未在[試算表](#configure-abac-spreadsheet)中指定任何規則的所有其他使用者群組都會被拒絕存取。 如果使用者不屬於任何已定義ABAC規則的群組，他們將無法存取任何資產。 如果部分使用者必須擁有所有資產的存取權（例如「管理員」），請在試算表中加入具有群組ID的群組，並指定該群組需要存取所有資產，讓Adobe能夠進行相應設定。

## 支援的規則建構 {#supported-rule-constructs}

* **邏輯運運算元**：
   * AND：所有條件都必須為true
   * 或：至少一個條件必須為true

* **比較運運算元**：
   * 等於(=)：檢查使用者或資產屬性是否符合值
   * 不等於(!=)：檢查使用者或資產屬性是否與值不符

當資產中繼資料欄位包含陣列（例如多個區域或標籤）時，等於是指包含邏輯，而不等於是指不包含邏輯。

這可讓您撰寫簡單且表達式的規則，例如ALLOW if region = emea和assetType != prototype AND標籤!=機密。

## 准則 {#guidelines-attribute-based-access-control}

下列准則同時適用於AI Assistant型和試算表型設定：

* ABAC規則僅適用於針對Content Hub核准的資產。 如需詳細資訊，請參閱[核准Content Hub的Assets](/help/assets/approve-assets-content-hub.md)。
* 請勿定義DENY規則。 一律將DENY規則轉換為ALLOW規則。 例如，如果區域= region = user-region DENY if assetType = prototype AND confidential = yes，則可以轉換為ALLOW if region = user-region AND （如果區域= region AND confidential != prototype OR confidential != yes）。
* ABAC規則會使用IMS群組ID （可在Admin Console中取得）套用至使用者群組。
* 您可以使用AEM as a Cloud Service作者環境設定資產的[核准目標](/help/assets/approve-assets-content-hub.md#set-approval-target)。 ABAC規則會套用至核准目標= Content Hub的已核准資產，因為核准目標=傳送適用於可用於傳送+ Content Hub的資產。 Assets標示為核准目標=傳遞對Content Hub中的所有人可見。
* 請確定ABAC規則中使用的中繼資料結構已正確定義，並可在AEM中使用。 提供AEM中定義在ABAC規則中參考之屬性的中繼資料結構或結構的完整路徑。 您可以選擇使用符合ABAC條件的範例資產建立測試資料夾，以協助驗證規則行為並準確評估存取權。
* 在註解中擷取規則的商業目的，即使條件已正確寫入，因為目的有助於驗證及修正邏輯（若有需要）。
* 確保用於存取規則（例如品牌、地區和產品）的中繼資料值在整個資產中保持一致。
* 從品牌型或區域型存取等關鍵使用案例開始。
* 使用AI助理定義規則時，請使用清除提示。 使用商業語言描述意圖，以便AI助理可以將其轉換為結構化規則。
* 為DRM設定的PDF授權檔案必須對所有使用者可見，以便他們在下載具有授權的資產時可以檢閱授權資訊。

## 常見問題 {#faqs-attribute-based-access-control-content-hub}

### 什麼是AEM Assets Content Hub中的屬性型存取控制(ABAC)？

AEM Assets Content Hub中的屬性型存取控制(ABAC)可讓管理員定義中繼資料型規則，以控制不同使用者群組對數位資產的存取層級。 存取許可權取決於資產中繼資料是否符合規則中指定的條件，允許對資產可見性進行精細的動態管理。

### 管理員如何在AEM Assets Content Hub中使用ABAC定義存取規則？

管理員會根據資產中繼資料（例如品牌或區域）建立條件，並將這些條件連結至特定的使用者群組ID，以定義存取規則。 這些規則會使用邏輯和比較運運算元，準確地指定哪些資產對哪些使用者群組可見。

### 在AEM Assets Content Hub中使用ABAC較之傳統檔案夾型許可權有哪些主要優點？

ABAC消除許可權對檔案夾結構的相依性，允許管理員上傳資產並回溯指派許可權，並減少所需的重複資產數量。 這麼做可改善資產完整性並簡化許可權管理，尤其是當資產需要與多個群組共用時。

### 管理員可以直接在AEM Assets Content Hub介面中設定ABAC規則嗎？

管理員可以使用Content Hub中的AI助理設定ABAC規則（如果為其組織啟用）。 他們也可以繼續透過Adobe支援使用試算表式工作流程。

### 在AEM Assets Content Hub中設定ABAC規則時，可以使用哪些型別的中繼資料條件？

AEM Assets Content Hub中的ABAC規則可以使用邏輯運運算元（例如AND和OR）以及比較運運算元（例如equals和not equals）。 規則中使用的中繼資料屬性必須正確定義，並可在AEM中繼資料結構中使用，而且可包含地區、品牌、產品、行銷活動、資產型別或發佈狀態等欄位。

### 為何AEM Assets Content Hub ABAC對於擁有大型團隊和多種資產需求的組織特別有用？

ABAC對於擁有大型團隊的組織非常有用，因為它可以根據使用者角色、地區、品牌或業務需求，啟用以規則為基礎的細微資產存取。 這可確保使用者只看到與其職責相關的資產，而不會手動指派許可權或過度重複資產。

### 管理員在將ABAC試算表提交給AEM Assets Content Hub支援之前，應如何為Adobe準備試算表？

管理員應在Adobe Admin Console中建立使用者群組、記下其群組ID、清楚定義試算表中每個群組的許可權和條件、確保所有中繼資料屬性正確對應至適當的結構描述，並使用註解欄來釐清每個規則的商業目的。