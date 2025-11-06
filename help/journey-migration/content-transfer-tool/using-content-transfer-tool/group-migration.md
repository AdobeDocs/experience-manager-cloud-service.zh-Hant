---
title: 群組移轉
description: AEM as a Cloud Service中的群組移轉概觀。
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1917'
ht-degree: 3%

---


# 群組移轉 {#group-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_groupmigration"
>title="群組移轉"
>abstract="內容轉移工具可協助您將現有 Adobe Experience Manager (AEM) 系統中的群組複製到 AEM as a Cloud Service。"

>[!NOTE]
>如需舊版的使用者對應工具，請參閱[舊版檔案](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)。

## 簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermigration"
>title="使用者未移轉"
>abstract="內容轉移工具不再移轉使用者。應在 Admin Console 中管理使用者。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="AEM Admin Console 文件"
>additional-url="https://adminconsole.adobe.com/" text="AEM Admin Console"

在轉換至Adobe Experience Manager (AEM) as a Cloud Service的過程中，群組必須從現有的AEM系統移轉至AEM as a Cloud Service。 此工作由「內容轉移工具」完成。

AEM as a Cloud Service的一項重大變更是完全整合使用Adobe ID來存取作者階層。 此程式需要使用[Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)來管理使用者和使用者群組。 使用者設定檔資訊會集中在Adobe Identity Management系統(IMS)中，可提供所有Adobe雲端應用程式的單一登入。 如需詳細資訊，請參閱[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management)。 由於此變更，使用者首次透過IMS登入時，系統會自動在AEM上建立。  因此，CTT不會將使用者移轉至雲端系統。  IMS使用者必須放置在IMS群組中，這些群組可以是移轉的群組，或放置在AEM群組(這些群組已獲得存取要移轉的AEM內容的許可權)中的新群組。  如此一來，雲端系統上的使用者就能在來源AEM系統上擁有相同的存取權。

## 群組移轉詳細資料 {#group-migration-detail}

「內容轉移工具」和Cloud Acceleration Manager會移轉與要移轉至雲端系統的內容相關聯的任何群組。 內容轉移工具會在提取程式期間從來源AEM系統複製所有群組，藉此執行此操作。 CAM擷取接著只選取和移轉特定群組：

* 如果群組位於已移轉內容的ACL或CUG原則上，該群組將會移轉，但以下列出一些例外。
* 有許多內建的群組已存在於目標雲端系統中；這些群組永遠都不會移轉。
   * 某些內建群組可能包含&#x200B;_非_&#x200B;內建的成員群組；移轉內容的ACL或CUG原則中參考的任何此類成員群組（直接成員或成員成員等）將會進行移轉，以確保屬於這些群組成員的使用者（直接或間接）維持其對移轉內容的存取權。
* 其他群組，例如在ACL或CUG原則中找不到的群組、在目標系統上的群組，以及目標系統上具有任何唯一性限制資料的群組，將不會進行移轉。

請注意，為群組記錄/報告的路徑只是觸發該群組移轉的第一個路徑，且該群組可能也在其他內容路徑上。

大部分已移轉的群組已設定為由IMS管理。  這表示IMS中具有相同名稱的群組將連結至AEM中的群組，而IMS群組中的任何IMS使用者都會成為AEM中的AEM使用者和群組成員。  這可讓這些使用者根據群組的ACL或CUG原則存取內容。

請注意，已移轉的群組不再被視為AEM的「本機群組」；在AEM中是IMS就緒的群組，雖然它們可能尚未存在於IMS中。  它們必須在IMS中另外重新建立，以便在AEM和IMS之間同步。  除了其他方法以外，可以透過Admin Console在IMS中個別或大量建立群組。  如需在Admin Console上個別或大量建立群組的詳細資訊，請參閱[管理使用者群組](https://helpx.adobe.com/tw/enterprise/using/user-groups.html)。

此IMS設定的例外情況是Assets集合和私人資料夾建立的群組。 在AEM上建立集合或私人資料夾時，會建立群組以供存取該內容；這類群組會移轉至雲端系統，但不會設定為由IMS管理。  若要將IMS使用者新增至這些群組，他們就必須在Assets UI的群組屬性頁面中新增使用者，且以個別或集體方式新增至其他IMS群組。


## 選擇退出群組移轉 {#group-migration-option}

CTT 3.0.20版及更新版本包含可停用群組移轉的選項。  這在OSGI主控台中設定如下：

* 開啟OSGI設定`(http://<server>/system/console/configMgr)`
* 按一下名為&#x200B;**內容轉移工具擷取服務組態**&#x200B;的組態
* 取消勾選&#x200B;**在移轉中包含群組**&#x200B;以停用群組移轉
* 按一下[儲存] **&#x200B;**，確定組態已儲存並在伺服器上啟用

停用此設定後，將不會移轉群組，而且不會有主體移轉報告或使用者報告（請參閱下文）。

## 主體移轉報告和使用者報告 {#principal-migration-report}

移轉期間若包含群組（預設），系統便會儲存「主體移轉報告」，當中會概述每個群組在移轉期間發生的情況。  若要在成功內嵌後下載此報表：

* 在CAM中，前往「內容轉移」並選取「擷取工作」。
* 按一下相關內嵌行上的省略符號(...)，然後選擇「檢視主體摘要」。
* 在出現的對話方塊中，從「下載檔案……」下的下拉式清單中選取「主體移轉報告」，然後按一下「下載」按鈕。
* 儲存產生的CSV檔案。

每個群組記錄的部分資訊為：

* 如果移轉，則為導致群組移轉的第一個ACL或CUG的路徑。
* 無論群組先前是否已移轉；如果目前的擷取為非擦去擷取，則某些群組可能已在先前的擷取期間移轉。
* 群組是否為內建群組；這些群組不會移轉，因為它們一律位於目標AEMaaCS環境。
* 如果群組不是移轉內容上ACL或CUG的一部分，則不會移轉該群組。
* 如果群組是本機群組(例如Assets集合建立的群組)，則可能已移轉該群組，而且在此案例中，「本機」一詞會新增到該群組的報表中。

在移轉期間，使用者不會移轉，但除非以某種方式擷取使用者，否則來源系統上的使用者 — 群組關係將會遺失。 擷取程式會以文字格式在使用者報告中擷取上述部分資訊，該報告位於主要移轉報告的結尾。

### 使用者報表 {#user-report}

在使用者報告區段中，會報告使用者（每行一個），以及其電子郵件地址和在此擷取期間移轉且啟用IMS的群組清單。  清單中不包含未移轉的群組、在上次內嵌期間移轉的群組或本機群組。   如果使用者不在任何已移轉的IMS啟用群組中，並且沒有額外的備註來指示它是特例（請參閱下面的&#x200B;**備註**），則該使用者&#x200B;_不會_&#x200B;出現在報表中。 與每個使用者一起報告的群組是使用者在來源系統中直接或間接身為成員的群組；由於來源系統中的群組可能巢狀化，而目標系統中的群組則否，因此此群組清單支援IMS中的新平面化群組結構。

如果擦除接著非擦除擷取，則非擦除擷取的使用者清單中的群組將只會在非擦除階段中移轉的群組。

#### 備註 {#user-report-notes}

除了每個使用者的群組之外，使用者報告中還有一個欄位，可提供關於使用者的附註（報告中也提供了附註含義的詳細說明）以供參考。  可能的注意事項包括：

* **附註 — A**&#x200B;直接在ACL中參照的使用者在其附註區段中會有&#x200B;*附註 — A*，因為這不是建議的使用案例或最佳作法。
* **Note-B**&#x200B;內建群組的直接成員使用者在其筆記區段中會有&#x200B;*Note-B*，因為這不是建議的使用案例或最佳做法。
* **Note-C**&#x200B;直接屬於已移轉本機群組(例如Assets集合建立的群組)之間接成員的使用者，其附註區段中會有&#x200B;*Note-C*，因為本機群組未設定為由IMS管理。

這些案例可以同時發生，也可以與前幾個案例同時發生。  _如需有關每個備註參照給每個使用者的群組的其他資訊，請查閱擷取記錄；它會為每個使用者報告此資訊。_

使用者報告會新增到主體移轉報告的結尾（因此是其中一部分） （請參閱下方的[最終摘要與報告](#final-summary-and-report)），讓客戶更全面瞭解群組與使用者及其關係。

## 大量上傳檔案 {#bulk-upload-files}

由於群組僅移轉至AEM as a Cloud Service，因此群組仍必須新增至IMS，才能在雲端中正確搭配AEM使用。 此外，使用者不會移轉，因此也需要將其新增至IMS。 CTT/CAM移轉工具不會執行此步驟，但擷取程式會建立兩個大量上傳檔案，一個供群組使用，一個供使用者使用。 您可以編輯這些檔案，然後將其與Admin Console的大量上傳功能搭配使用，根據您的AEM群組和使用者來建立IMS群組和使用者。

如需有關如何使用Admin Console大量上傳檔案來建立使用者和群組的詳細資訊，請參閱[大量群組和使用者上傳至IMS](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md)。

另請參閱[管理使用者](https://helpx.adobe.com/ca/enterprise/using/users.html)，以取得有關管理AEM as a Cloud Service使用者的其他詳細資訊。

## 其他考量事項 {#additional-considerations}

* 如果設定了&#x200B;**在內嵌之前擦除雲端執行個體上的現有內容**，則會刪除先前傳輸至Cloud Service執行個體的群組以及整個現有存放庫；將建立新存放庫，並內嵌內容。 此程式也會重設所有設定，包括目標Cloud Service執行個體的許可權，且對於新增至&#x200B;**管理員**&#x200B;群組的任何使用者而言皆為真。 必須將管理員使用者重新新增到&#x200B;**管理員**&#x200B;群組，才能擷取CTT/CAM擷取的存取權杖。
* 執行非擦去擷取時（**未設定擦去現有內容**），如果內容未傳輸，因為在上次傳輸後內容未變更，則與該內容關聯的群組也不會傳輸。 即使群組在來源系統上已變更，此規則仍為真。 這是因為群組只會隨著與其相關聯的內容一起移轉。 因此，在此情況下，任何屬於來源系統群組成員的群組，都不會進行移轉，除非這些群組屬於正在移轉的不同群組，或位於正在移轉的不同內容的ACL中。 若要在之後移轉這些群組，請考慮使用套件、從目標中刪除群組並重新移轉相關內容，或使用擦去內嵌重新移轉。
* 在非擦去擷取期間，如果來源AEM執行個體和目標AEM Cloud Service執行個體上存在具有任何相同唯一性限制資料（rep:principalName、rep:authorizableId、jcr:uuid或rep:externalId）的群組，則有問題的群組是&#x200B;_未_&#x200B;移轉，而雲端系統上先前存在的群組保持不變。 這會記錄在「主要移轉報表」中。
* 請參閱[移轉封閉式使用者群組](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md)，以了解封閉式使用者群組(CUG)原則中所使用群組的額外考量事項。

## 最終摘要與報告

擷取和內嵌成功完成後，就會產生一份報表，顯示群組移轉詳細資訊。 如需詳細資訊，請參閱[如何驗證群組移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration)。
