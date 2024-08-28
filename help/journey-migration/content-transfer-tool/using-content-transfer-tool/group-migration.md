---
title: 群組移轉
description: AEM as a Cloud Service中的群組移轉概觀。
exl-id: 4a35fc46-f641-46a4-b3ff-080d090c593b
source-git-commit: e5fd1b351047213adbb83ef1d1722352958ce823
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 0%

---


# 群組移轉 {#group-migration}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_groupmigration"
>title="群組移轉"
>abstract="「內容轉移工具」可協助您將群組從現有的Adobe Experience Manager (AEM)系統複製到AEM as a Cloud Service。"

>[!NOTE]
>如需舊版的使用者對應工具，請參閱[舊版檔案](/help/journey-migration/content-transfer-tool/user-mapping-tool-legacy/considerations-user-mapping-tool-legacy.md)。

## 簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_usermigration"
>title="使用者未移轉"
>abstract="「內容轉移工具」不再移轉使用者。 應以Admin Console管理使用者。"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/admin-console" text="AEMAdmin Console檔案"
>additional-url="https://adminconsole.adobe.com/" text="AEMAdmin Console"
>
在轉換至Adobe Experience Manager (AEM)as a Cloud Service的過程中，群組必須從現有的AEM系統移轉至AEM as a Cloud Service。 此工作由「內容轉移工具」完成。

AEM as a Cloud Service的一項重大變更是完全整合式使用AdobeID來存取作者階層。 此程式需要使用[Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)來管理使用者和使用者群組。 使用者設定檔資訊會集中在AdobeIdentity Management系統(IMS)中，可提供所有Adobe雲端應用程式的單一登入。 如需詳細資訊，請參閱[Identity Management](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/overview/what-is-new-and-different.html#identity-management)。 由於此變更，使用者首次透過IMS登入時，系統會自動在AEM上建立。  因此，CTT不會將使用者移轉至雲端系統。  IMS使用者必須放置在IMS群組中，這些群組可以是移轉的群組，或是放置在AEM群組(這些群組已獲得存取要移轉的AEM內容的許可權)中的新群組。  如此一來，雲端系統上的使用者將可擁有其來源AEM系統上的相同存取權。

## 群組移轉詳細資料 {#group-migration-detail}

「內容轉移工具」和Cloud Acceleration Manager會移轉與要移轉至雲端系統的內容相關聯的任何群組。 「內容轉移工具」會在提取程式期間從來源AEM系統複製所有群組，以達成此目的。 CAM擷取接著只選取和移轉特定群組：

* 有許多內建的群組已存在於目標雲端系統中；這些群組永遠都不會移轉。
* 任何內建群組的直接成員群組（在已移轉內容的ACL或CUG原則中直接或間接參照）將會移轉，以確保使用者是這類群組的直接或間接成員，能夠繼續存取已移轉的內容。
* 如果群組位於已移轉內容的ACL或CUG原則上，則會移轉該群組。
* 其他群組，例如在ACL或CUG原則中找不到的群組、在目標系統上的群組，以及目標系統上具有任何唯一性限制資料的群組，將不會進行移轉。

請注意，為群組記錄/報告的路徑只是觸發該群組移轉的第一個路徑，且該群組可能也在其他內容路徑上。

大部分已移轉的群組已設定為由IMS管理。  這表示IMS中具有相同名稱的群組將連結至AEM中的群組，而IMS群組中的任何IMS使用者都會成為AEM中的AEM使用者和群組成員。  這可讓這些使用者根據群組的ACL或CUG原則存取內容。

此IMS設定的例外情況是Assets集合建立的群組。 在AEM上建立集合時，會建立群組以供存取該集合；此類群組會移轉至雲端系統，但不會設定為由IMS管理。  若要將IMS使用者新增至這些群組，他們就必須在Assets UI的群組屬性頁面中新增使用者，且以個別或集體方式新增至其他IMS群組。


## 選擇退出群組移轉 {#group-migration-option}

CTT 3.0.20版及更新版本包含可停用群組移轉的選項。  這在OSGI主控台中設定如下：

* 開啟OSGI設定`(http://<server> /system/console/configMgr)`
* 按一下名為&#x200B;**內容轉移工具擷取服務組態**&#x200B;的組態
* 取消勾選&#x200B;**在移轉中包含群組**&#x200B;以停用群組移轉
* 按一下[儲存] ****，確定組態已儲存並在伺服器上啟用

停用此設定後，將不會移轉群組，而且不會有主體移轉報告或使用者報告。

## 使用者報表 {#user-report}

移轉期間不會移轉使用者，但來源系統上的使用者 — 群組關係會遺失，除非以某種方式擷取這些使用者。  使用者報告會以文字格式在使用者報告中擷取其中的一些資訊。 其中會報告每個使用者（每行一個）及其所屬的群組清單（但未移轉的群組不會放在此清單中），除非其群組清單是空的，在此情況下，使用者不會出現。 與每個使用者一起報告的群組是使用者直接或間接在來源系統中的成員；由於來源系統中的群組可能巢狀化，而目標系統中的群組則否，因此此群組清單支援IMS中的新平面化群組結構。

如果擦除接著非擦除擷取，使用者清單中的群組將包含在任一階段中移轉的群組。

除了每個使用者的群組之外，報告中還有一個欄位，可以在其中為使用者新增附註（報告中也提供了附註含義的詳細說明）。  可能的附註包括：

* 直接在ACL中參照的使用者在其筆記區段中將會有&#x200B;*Note-A*，因為這不是建議的使用案例或最佳實務。
* 內建群組的直接成員使用者在其筆記區段中將會有&#x200B;*Note-B*，因為這不是建議的使用案例或最佳實務。

這些案例可以同時發生，也可以與前幾個案例同時發生。

使用者報告會新增到主體移轉報告的結尾（因此是其中一部分） （請參閱下方的[最終摘要與報告](#final-summary-and-report)）。

## 其他考量事項 {#additional-considerations}

* 如果設定了&#x200B;**在內嵌之前擦除雲端執行個體上的現有內容**，則會刪除先前傳輸至Cloud Service執行個體的群組以及整個現有存放庫；將建立新存放庫，並內嵌內容。 此程式也會重設所有設定，包括目標Cloud Service執行個體的許可權，且對於新增至&#x200B;**管理員**&#x200B;群組的任何使用者而言皆為true。 必須將管理員使用者重新新增到&#x200B;**管理員**&#x200B;群組，才能擷取CTT/CAM擷取的存取權杖。
* 執行非擦去擷取時（**未設定擦去現有內容**），如果內容未傳輸，因為在上次傳輸後內容未變更，則與該內容關聯的群組也不會傳輸。 即使群組在來源系統上已變更，此規則仍為真。 這是因為群組只會隨著與其相關聯的內容一起移轉。 因此，在此情況下，任何屬於來源系統群組成員的群組，都不會進行移轉，除非這些群組屬於正在移轉的不同群組，或位於正在移轉的不同內容的ACL中。 若要在之後移轉這些群組，請考慮使用套件、從目標中刪除群組並重新移轉相關內容，或使用擦去內嵌重新移轉。
* 在非擦去擷取期間，如果來源AEM執行個體和目標AEM Cloud Service執行個體上存在具有任何相同唯一性限制資料（rep：principalName、rep：authorizableId、jcr：uuid或rep：externalId）的群組，則有問題的群組是&#x200B;_未_&#x200B;移轉，而雲端系統上先前存在的群組保持不變。 這會記錄在「主要移轉報表」中。
* 請參閱[移轉封閉式使用者群組](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/closed-user-groups-migration.md)，以了解封閉式使用者群組(CUG)原則中所使用群組的額外考量事項。

## 最終摘要與報告

擷取和內嵌成功完成後，就會產生一份報表，顯示群組移轉詳細資訊。 如需詳細資訊，請參閱[如何驗證群組移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/validating-content-transfers.md#how-to-validate-group-migration)。
