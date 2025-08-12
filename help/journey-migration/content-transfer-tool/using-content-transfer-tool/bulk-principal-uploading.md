---
title: 使用CTT後將主體大量上傳到IMS
description: 群組和使用者的大量上傳檔案概觀，以及如何在 Admin Console 使用以建立群組和 IMS 使用者。
exl-id: 43ebd6f1-1492-461a-8d9b-2b55dcde9052
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 3%

---

# 使用 CTT 後將主體大量上傳至 IMS {#bulk-principal-uploading}

>[!CONTEXTUALHELP]
>id="bulk-principal-uploading"
>title="主體大量上傳"
>abstract="群組和使用者的大量上傳檔案概觀，以及如何在 Admin Console 使用以建立群組和 IMS 使用者。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="AEM Admin Console 文件"
>additional-url="https://adminconsole.adobe.com/" text="AEM Admin Console"

## 簡介 {#introduction}

使用CTT和CAM將內容移轉至雲端，會在AEM雲端例項上建立群組，但無法進行任何動作將群組或使用者放入IMS中。 客戶必須存在於IMS中才能正確管理。 幸運的是，Admin Console提供了大量建立IMS群組和使用者的功能。 CAM內嵌會儲存大量建立的輸入檔案，協助此程式，讓客戶完成此Admin Console動作，作為其整體移轉程式的一部分。 會建立兩種大量上傳檔案：一種適用於群組，另一種適用於使用者。

另請參閱[管理使用者](https://helpx.adobe.com/tw/enterprise/using/users.html)，以取得有關管理AEM as a Cloud Service使用者的其他詳細資訊。

## 上傳檔案的一般規則 {#rules}

對於編輯及使用這兩種上傳檔案，有一些一般准則：

* 必須先授予Admin Console的管理員存取權，才能依照這些指示操作。
* 請注意，在IMS中建立使用者和群組有幾種不同的方式。  請參閱[Adobe Experience Manager as a Cloud Service的IMS支援](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/security/ims-support)，瞭解所有可用的選項。  此處僅說明Admin Console大量上傳方法。
* IMS中可能有三種身分型別：Adobe ID、Enterprise ID和Federated ID。  此頁面上的指示僅適用於&#x200B;**Adobe ID**。  如果您需要使用Enterprise ID或Federated ID，請參閱完整的[Admin Console檔案](https://helpx.adobe.com/ca/enterprise/using/admin-console.html)以及[Admin Console大量群組上傳](https://helpx.adobe.com/ca/enterprise/using/user-groups.html)和[Admin Console大量使用者上傳](https://helpx.adobe.com/ca/enterprise/using/bulk-upload-users.html)的特定檔案。  上傳檔案的規格在這兩種身分型別中有些不同。
* 如果單一CSV欄位允許多個專案（例如多個產品設定檔、多個群組或多個管理員），這些專案必須包含雙引號並以逗號分隔，即`"profile 1,profile 2"`。

   * 在這種情況下，可以使用單引號而不是雙引號，但在Microsoft Excel中編輯檔案可能會導致剖析問題。 如果使用Excel編輯這些檔案，請務必使用雙引號而非單引號。

## 大量群組上傳 {#group-upload}

### 使用案例：群組已移轉至AEM as a Cloud Service，但這些群組不存在於IMS/Admin Console中，因此需要透過Admin Console將其上傳至IMS。

若要在執行CTT/CAM移轉之後使用Admin Console的大量群組上傳功能，請遵循下列步驟：

1. 從CAM下載主體群組檔案

   1. 在CAM中，移至&#x200B;**內容轉移**&#x200B;並選取&#x200B;**擷取工作**。
   1. 按一下相關內嵌行上的省略符號(...)，然後選擇&#x200B;**檢視主體摘要**。
   1. 在出現的對話方塊上，從&#x200B;**下載檔案……**&#x200B;下的下拉式清單中選取&#x200B;**大量群組檔案**，然後按一下&#x200B;**下載**&#x200B;按鈕。
   1. 儲存產生的CSV檔案。

1. 編輯大量群組檔案

   * 每一行代表要上傳的群組，且有四個欄位（欄位的名稱構成檔案的第一行）：

      * _使用者群組名稱_ — 需要群組名稱，最多可包含255個字元。  IMS和AEM中的此群組名稱必須相同
      * _描述_ — 此欄位是選擇性的，最多可包含255個字元
      * _使用者群組管理員_ — 此欄位中必須至少包含一個群組管理員。 以逗號分隔每個管理員，並將清單放在引號中，可指派多個管理員。 每個管理員的專案必須包含使用者的身分型別，後面跟一個連字型大小，然後是電子郵件地址。  例如
        `"Adobe ID-myAdmin@example.com,Adobe ID-myOtherAdmin@example.com"`。請勿在管理員間的逗號後面加上空格。 您無法將目前不屬於組織的使用者（管理員）納入Admin Console
      * _已指派的產品設定檔_ — 此欄位是選擇性的。 您可以指派多個產品設定檔，方法是以逗號分隔每個設定檔，並將清單以引號括住。 不過，您必須已經為組織設定您所包含的產品設定檔。 請確定您指定產品設定檔名稱，而非產品名稱。  指派給群組的產品設定檔成員資格將由該群組中的所有使用者繼承。  若要尋找產品設定檔：

         1. 前往Admin Console
         1. 尋找您的產品(即Adobe Experience Manager as a Cloud Service)，然後按一下它
         1. 找到您的環境（例項），然後按一下它
         1. 列出產品設定檔，然後按一下您的AEM環境設定檔。 產品設定檔位於頂端，即&quot;_AEM使用者 — 作者 — 方案12345 — 環境012345_&quot;。

   * 編輯CSV時，某些應用程式可能會在儲存時新增其他引號，導致處理失敗。 在簡單的文字編輯器中檢查原始CSV是建議的做法，以確保每個欄位都只有一個開頭和結尾引號（而且不應「是智慧型引號」）。

1. 在Admin Console中上傳大量群組檔案

   1. 在Admin Console中，移至&#x200B;**使用者**，然後移至&#x200B;**使用者群組**
   1. 在右側按一下「……」按鈕。 從功能表中選擇&#x200B;**以CSV新增使用者群組**，然後選擇您要上傳的CSV。 按一下&#x200B;**上傳**
   1. 您會收到回應，指出CSV已上傳(至Admin Console)，但尚未匯入至IMS
   1. 移至相同的「……」功能表，然後選擇&#x200B;**大量作業結果**。 它會顯示大量上傳嘗試的清單，並告訴您（在&#x200B;**狀態**&#x200B;下）大量上傳正在處理、成功或失敗

      * 它一開始會顯示處理中，表示尚未完成
      * 成功完成後，按一下連結&#x200B;**新增使用者群組**&#x200B;以檢視每行的簡單狀態訊息。
      * 如果失敗，請按一下&#x200B;**檔案**&#x200B;下的小型圖示，它會提供一些失敗原因的詳細資訊。  從第1列開始參照群組行號。
1. 使用Admin Console驗證變更。

## 大量使用者上傳和編輯 {#bulk-user}

Admin Console包含上傳和編輯使用者詳細資訊的兩個個別動作。 以下提供新增使用者至IMS的指示。 編輯現有IMS使用者的指示位於下列名為[大量使用者編輯](#user-edit)的區段。

### 大量使用者上傳 {#user-upload}

#### 使用案例：群組已移轉至AEM as a Cloud Service，並透過大量上傳或其他方法上傳。  使用者可能不在IMS/Admin Console中，因此需要透過Admin Console將其上傳並連結至IMS中的群組。

>[!NOTE]
>
>如果使用者在&#x200B;**大量使用者上傳**&#x200B;檔案的同一個內嵌期間所內嵌的群組中，則會顯示該檔案中的使用者。 如果使用者直接位於已移轉內容的ACL或CUG上，或是內建群組或本機群組的成員（位於已移轉內容的ACL或CUG上），也可能顯示此訊息。 如需這些情況的詳細資訊，請參閱[群組移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)。

若要使用Admin Console的大量使用者上傳功能，請遵循下列步驟：

1. 從CAM下載大量使用者檔案
   1. 在CAM中，移至&#x200B;**內容轉移**&#x200B;並選取&#x200B;**擷取工作**。
   1. 按一下相關內嵌行上的省略符號(...)，然後選擇&#x200B;**檢視主體摘要**。
   1. 在出現的對話方塊上，從&#x200B;**下載檔案……**&#x200B;下的下拉式清單中選取&#x200B;**大量使用者檔案**，然後按一下&#x200B;**下載**&#x200B;按鈕。
   1. 儲存產生的CSV檔案
1. 編輯大量使用者檔案
   * 每一行代表要上傳的使用者，共有十五個欄位（欄位的名稱構成檔案的第一行）。 有些欄位是選用欄位，此處不說明。 請參閱[大量使用者CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)。  欄位包括：

      * _身分型別_ — 選擇性。  若未指定，則會建立為Adobe ID
      * _使用者名稱_ — 選擇性，不用於Adobe ID上傳
      * _網域_ — 選擇性，不用於Adobe ID上傳
      * _電子郵件_ — 必填。  該電子郵件地址將在使用者首次登入時用於驗證
      * _名字_ — 選擇性。  應該使用，因為它會以姓氏出現在數個位置
      * _姓氏_ — 選擇性。  應該使用，因為它出現在多個位置
      * _國家/地區代碼_ — 選擇性，不用於Adobe ID上傳
      * _ID_ — 選用，不用於Adobe ID上傳
      * _產品組態_ — 選擇性。 此欄位也將繼承自使用者所屬的任何群組
      * _管理員角色_ — 選擇性。 如果使用者是管理員，請使用此欄位。 如需詳細資訊，請參閱[大量使用者CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)
      * _已管理的產品組態_ — 選擇性。  如需詳細資訊，請參閱[大量使用者CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)。 此欄位也將繼承自使用者所屬的任何群組
      * _使用者群組_ — 選擇性。 應指派使用者作為成員的群組清單。 每個群組都必須是現有的IMS群組。 從CAM下載大量使用者檔案時，此欄位會預先填入使用者在移轉前（直接或間接）身為其IMS啟用群組成員的名稱
      * _已管理的使用者群組_ — 選擇性。  如需詳細資訊，請參閱[大量使用者CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)。 此欄位也將繼承自使用者所屬的任何群組
      * _管理的產品_ — 選擇性。  如需詳細資訊，請參閱[大量使用者CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)。 此欄位也將繼承自使用者所屬的任何群組
      * _管理的合約_ — 選擇性。  如需詳細資訊，請參閱[大量使用者CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)
      * _開發人員存取權_ — 選擇性。  如需詳細資訊，請參閱[大量使用者CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)
      * _自動指派的產品_ — 選擇性。  如需詳細資訊，請參閱[大量使用者CSV格式](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html#csv-format)

   * 編輯CSV時，某些應用程式可能會在儲存時新增其他引號，導致處理失敗。 在簡單的文字編輯器中檢查原始CSV是建議的做法，以確保每個欄位都只有一個開頭和結尾引號（而且不應「是智慧型引號」）

1. 使用Admin Console匯入大量使用者檔案

   1. 在Admin Console中，前往使用者
   1. 按一下&#x200B;**透過CSV新增使用者**&#x200B;按鈕
   1. 拖放或選取從CAM下載的大量使用者CSV檔案
   1. 按一下&#x200B;**上傳**&#x200B;按鈕
   1. 您會收到回應，指出CSV已上傳(至Admin Console)，但尚未匯入至IMS。
   1. 移至右側的「……」功能表，然後選擇&#x200B;**大量作業結果**。  它會顯示大量上傳嘗試的清單，並顯示（在&#x200B;**狀態**&#x200B;下）大量上傳正在處理、成功或失敗。

      * 它一開始會顯示處理中，表示尚未完成
      * 成功完成後，按一下連結&#x200B;**新增使用者**&#x200B;以檢視每行的簡單狀態訊息
      * 如果失敗，請按一下&#x200B;**檔案**&#x200B;下的小圖示，它會提供您更多失敗原因的資訊。 從第1列開始參照使用者行號。

1. 使用Admin Console驗證您的變更。

>[!NOTE]
>
>非清除擷取後，先前移轉並在IMS中建立的使用者可能會出現在大量使用者上傳檔案中。 這可能有很多原因。 在這種情況下，再次上傳使用者將失敗。 請改為嘗試從大量使用者上傳檔案中移除使用者，如果需要將使用者新增到不同的群組，請依照以下所述使用大量使用者編輯檔案。

### 大量使用者編輯 {#user-edit}

#### 使用案例：群組和使用者已移轉至AEM as a Cloud Service，並透過大量上傳或其他方法上傳。 現在，需要一次對多個使用者進行一些變更，例如將其新增到現有的IMS群組。

若要使用Admin Console的大量使用者編輯功能，請遵循下列步驟：

1. 從管理控制檯下載大量使用者檔案

   1. 在Admin Console中，前往使用者
   1. 在右側按一下「……」按鈕。  從功能表選擇&#x200B;**以CSV編輯使用者詳細資訊**
   1. 按一下&#x200B;**下載CSV範本**&#x200B;並選擇&#x200B;**目前的使用者**。  CSV檔案應該會顯示在您本機的「下載」資料夾中。

1. 編輯大量使用者檔案

   1. 在Admin Console中，前往使用者
   1. 使用文字編輯器（建議）或試算表應用程式（例如Excel）來編輯CSV檔案。 使用應用程式可能會對資料造成無法預測的變更，因此建議在進行所有編輯之後，應使用文字編輯器來驗證檔案的格式
   1. 此檔案中欄位的說明與上述相同，位於「大量使用者上傳」下
   1. 移除所有未編輯的使用者
   1. 如果您變更使用者群組欄位，請保留目前的群組並根據需要新增群組。 如果您移除現有群組，系統會將使用者從IMS的該群組中移除
   1. 編輯CSV時，某些應用程式可能會在儲存時新增其他引號，導致處理失敗。 在簡單的文字編輯器中檢查原始CSV檔案是建議的做法，以確保每個欄位都只有一個開頭和結尾引號（而且不應該是「智慧引號」）

1. 在Admin Console中上傳大量使用者檔案

   1. 在Admin Console中，前往使用者
   1. 在右側按一下「……」按鈕。 從功能表選擇&#x200B;**以CSV編輯使用者詳細資訊**
   1. 拖放或選取已編輯的大量使用者CSV檔案
   1. 按一下「上傳」按鈕
   1. 您會收到回應，指出CSV已上傳(至Admin Console)，但尚未匯入至IMS
   1. 移至右側的「……」功能表，然後選擇&#x200B;**大量作業結果**。 它會向您顯示大量上傳嘗試的清單，並告訴您（在「狀態」下）大量上傳正在處理、成功或失敗。

      * 它一開始會顯示處理中，表示尚未完成
      * 成功完成後，按一下&#x200B;**編輯使用者詳細資料**&#x200B;連結，檢視每行的簡單狀態訊息
      * 如果失敗，請按一下&#x200B;**檔案**&#x200B;下的小圖示，它會顯示一些失敗原因的詳細資訊。 從第1列開始參照使用者行號。

1. 使用Admin Console驗證變更。
