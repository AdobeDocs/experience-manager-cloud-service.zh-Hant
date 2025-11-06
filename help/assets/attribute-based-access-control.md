---
title: 屬性型存取控制
description: 瞭解如何啟用屬性型存取控制來定義中繼資料型規則，以定義Content Hub中可用資產的存取層級
role: Admin
exl-id: 05f54b05-40b8-4a6c-af8f-5c3f7a2089d4
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 5%

---

# 屬性型存取控制 {#attribute-based-access-control}

屬性型存取控制(ABAC)可讓Content Hub管理員定義中繼資料型規則，以定義Content Hub中可用資產的存取層級。

組織的管理員會為對應至群組ID的使用者群組定義規則。 規則是[邏輯運運算元和比較運運算元的組合](#supported-rule-constructs)，管理員可定義任意數量的規則，以便在Content Hub中管理資產存取許可權。

規則是根據中繼資料，而且如果規則中定義的條件符合資產中繼資料，資產就會顯示給使用者群組。 Content Hub會掃描&#x200B;**所有Assets**&#x200B;和&#x200B;**集合**&#x200B;內所有可用資產的資產中繼資料（包括自訂中繼資料），將結果顯示給使用者群組。

例如，當資產中繼資料符合「品牌=品牌X」和「地區= EMEA或美洲」時，允許存取群組識別碼為1011的使用者群組。 Content Hub只會顯示識別碼= 1011且品牌= `Brand X`且地區= `EMEA`或`Americas`之使用者群組的資產。

屬性式存取控制的一些主要優點包括：

* 除去對資料夾結構的權限相依性

* 讓管理員能夠上傳資產並回溯性判定權限結構

* 減少重複的數量，提高資產完整性。當相同的資產與不同的群組共用時，資料夾型權限需要進行重複。

## 如何啟用以屬性為基礎的存取控制？ {#enable-attribute-based-access-control}

截至目前，您無法使用Content Hub使用者介面自行建立屬性型存取控制規則。

按一下&#x200B;**下載試算表**，即可下載試算表中規則並加以定義。 建立Adobe支援票證，並將試算表中定義的規則提供給Adobe。

[!BADGE 下載試算表]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/ABAC_Get_Started_Template.xlsx"}


使用本文定義的方針，在試算表中定義規則。

<!--

>[!IMPORTANT]
>
> After defining the rules, navigate to the **Validation Errors** tab of the spreadsheet and click **Run ABAC Validations**. **All validations passed** message confirms that you can provide the defined rules to Adobe.

-->

## 以屬性為基礎的存取控制使用案例範例 {#example-metadata-based-rules}

為了支援大規模行銷推出，地區和品牌的不同團隊成員需要存取數位資產。 每個角色都有根據地區和品牌的特定範圍。 ABAC會透過資產中繼資料自動強制執行這些規則。 下表說明此使用案例的不同角色型別以及套用的規則：

| 人物誌 | 角色 | 角色說明 | 群組識別碼 | ABAC規則 |
|---------------------|----------------|-----------------|------------|------------|
| John | EMEA行銷負責人 | 監督EMEA地區所有品牌的行銷執行。 需要存取所有針對EMEA市場之品牌的已核准資產。 | 群組 — 歐洲、中東及非洲地區 — 行銷 | 地區= &quot;EMEA&quot; |
| Mike | APAC行銷負責人 | 監督APAC中所有品牌的行銷執行。 需要存取專為APAC市場設計的所有品牌的已核准資產。 | group-apac-marketing | 地區= &quot;APAC&quot; |
| Sophie | 品牌X管理員(EMEA) | 管理EMEA地區的X品牌識別。 只需要看到針對EMEA市場量身打造的Brand X核准內容。 | group-emea-brandx | 地區= &quot;EMEA&quot; &amp;&amp; brand = &quot;Brand X&quot; |
| Tom | 品牌Y管理員(APAC) | 在APAC中管理Y品牌識別。 只需要看到Brand Y核准的專為APAC市場量身打造的內容。 | group-apac-brandy | 地區= &quot;APAC&quot; &amp;&amp; brand = &quot;Brand Y&quot; |

使用這些規則，Content Hub管理員可以：

* **精細、規則型存取**：使用者只會看到與其地區和品牌相關的資產 — 沒有手動許可權指派。

* **緊密的全球共同作業**：區域和品牌團隊同時運作，不會發生存取衝突。

* **可擴充且符合未來的校訂許可權**：隨著新地區或品牌的加入，可以根據中繼資料更新規則。

>[!IMPORTANT]
>
> 根據預設，所有其他使用者群組（未以[試算表](#enable-attribute-based-access-control)中的任何規則指定）都會被拒絕存取。 如果使用者不屬於任何已定義ABAC規則的群組，他們將無法存取任何資產。 如果您需要讓某些使用者擁有所有資產的存取權（例如「管理員」），則試算表中必須提及具有群組ID的群組，並提供此特定群組需要存取所有資產的詳細資料，而Adobe會為您進行設定。


## 支援的規則建構 {#supported-rule-constructs}

* **邏輯運運算元**：
   * AND：所有條件都必須為true
   * 或：至少一個條件必須為true
* **比較運運算元**：
   * 等於(=)：檢查使用者或資產屬性是否符合值
   * 不等於(！=)：檢查使用者或資產屬性是否與值不符

當資產中繼資料欄位包含陣列（例如，多個區域或標籤）時，`Equals`會參照`contains`邏輯，`Not Equals`會參照`does not contain`邏輯。

這可讓您編寫簡單且有表現力的規則，例如：如果區域= emea和assetType ，則允許！=原型和標籤！=機密。

## 准則 {#guidelines-attribute-based-access-control}

* ABAC規則僅適用於針對Content Hub核准的資產。 如需詳細資訊，請參閱[核准Content Hub的Assets](/help/assets/approve-assets-content-hub.md)。

* 不要授予DENY規則，而是一律將DENY轉換為ALLOW規則。 例如，`ALLOW if region = <user-region> DENY if assetType = prototype AND confidential = yes`可以轉換為`ALLOW if region = <user-region> AND (assetType != prototype OR confidential != yes)`。

* ABAC規則會使用IMS群組ID (可在Admin Console中取得)套用至使用者群組。


* 您可以使用AEM as a Cloud Service作者環境設定資產的[核准目標](/help/assets/approve-assets-content-hub.md#set-approval-target)。 ABAC規則已套用至核准目標= `Content Hub`的已核准資產，因為核准目標= `Delivery`適用於可用於`Delivery` + `Content Hub`的資產。 標示為核准目標的Assets = `Delivery`對內容中心中的所有人可見。

* 請確定ABAC規則中使用的中繼資料結構已正確定義，並可在AEM中使用。 提供AEM中定義在ABAC規則中參照之屬性的中繼資料結構的完整路徑。 您可以選擇建立測試資料夾，其中包含一些具有符合ABAC條件的中繼資料值的範例資產。 這有助於驗證規則行為並準確評估存取權。

* 擷取評論中規則的商業目的，無論條件是否正確寫入，因為目的可協助我們驗證並修正邏輯（若有需要）。

* 設定為DRM的授權PDF檔案必須對所有人可見，以便使用者在使用授權下載資產時能夠看到這些檔案。
