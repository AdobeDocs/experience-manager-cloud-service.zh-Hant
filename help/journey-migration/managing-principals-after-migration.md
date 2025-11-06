---
title: 遷移後管理主體
description: 了解如何在 IMS 和 AEM 中設定使用者和群組
exl-id: 46c4abfb-7e28-4f18-a6d4-f729dd42ea7b
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 100%

---

# 遷移後管理主體 {#managing-principals-after-migration}

>[!CONTEXTUALHELP]
>id="managing-principals"
>title="遷移後管理主體"
>abstract="了解如何在 IMS 和 AEM 中設定使用者和群組"

本文件說明客戶若希望其使用者和群組能搭配其 AEM as a Cloud Service 環境，則在 IMS 和 AEM 中設定時應採取的高層級步驟。

如需群組移轉和每次攝取時可用的主體移轉報告相關資訊，請參閱「[群組移轉](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)」。

如需在 Admin Console 中使用大量群組和使用者檔案的操作指南，請參閱「[使用 CTT 後將主體大量上傳至 IMS](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/bulk-principal-uploading.md)」。

## 管理主體 {#managing-principals}

對於 AEM as a Cloud Service，必須主要使用 Admin Console 來管理使用者和群組。考慮進行遷移時，其中的一些任務可以在內容遷移實作之前執行。基本上，在以下主要任務群組中

* 在 IMS 中建立使用者和群組
* 在 IMS 中將使用者指派至群組
* 將 IMS 群組指派至 AEM 群組 (如有必要)

前兩項可以在內容移轉之前或之後進行。這些步驟僅會影響 IMS 中的使用者和群組，可能包含與外部 IDP (例如 Active Directory 或 LDAP) 的整合。關於這些步驟的說明，請參閱[透過 Admin Console 管理 IMS 中的主體](/help/journey-migration/managing-principals.md)。

一旦內容遷移到 AEM as a Cloud Service 環境，即可執行第三步驟。

### 遷移群組

在遷移的攝取階段，如果需要滿足遷移內容的 ACL 或 CUG 原則，就會遷移群組。請參閱[群組遷移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md)以了解更多詳細資訊。

移轉的群組 (非透過資產集合或私人資料夾建立的群組；請參閱下方的「集合」和「私人資料夾」) 會設定為 IMS 群組。這表示在 IMS 中建立的任何同名群組 (例如透過 Admin Console) 都會連結到 AEM 中的群組，而且屬於 IMS 群組成員的使用者也將成為 AEM 中群組的成員。為了達成這項連結，也必須先在 IMS 中建立群組。使用 Admin Console 在 AEM 執行個體中單獨或大量建立群組，如[透過 Admin Console 管理 IMS 中的主體](/help/journey-migration/managing-principals.md)內容所述。

使用 AEM 安全性使用者介面將 IMS 群組指派到本機 AEM 群組。若要進行這項操作，請前往 AEM 的「工具」頁面，按一下「安全性」，並選擇「群組」。

### IMS 使用者

由於使用者未遷移，因此必須在 IMS 中建立使用者，才能在 AEM 中加以使用。有數種方法可以達到此目的，但重要的是，所建立的使用者應指派到正確的 IMS 群組，使用者才能對他們在先前 AEM 系統中擁有的內容具有相同的存取權。可用於此目的的工具之一是 Admin Console 中的大量上傳功能；使用大量上傳工具可上傳使用者及其必須隸屬的群組。執行此操作之前，必須先在 IMS 中建立群組，如上所述。

若要了解每位使用者應屬於哪些群組，您可以運用使用者報告 (請參閱[群組遷移](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/group-migration.md))。此報告列出每位使用者應隸屬的群組，且此清單通常會包含在大量使用者輸入檔案中，以便能與 Admin Console 的大量上傳功能一起使用。

### 集合和私人資料夾

建立資產集合或私人資料夾，也會自動建立一些群組來管理對該資產內容的存取權。如果在已移轉的內容中提及這些群組，便會移轉這些群組，但這些群組並未設定為直接連結到 IMS 群組；在 AEM 中，這些群組仍然是「本機群組」，而且無法透過 IMS 進行管理。

由於這些群組不在 IMS 中，因此無法使用大量上傳工具建立使用者作為其直接成員。同樣位於 AEM 中的 IMS 使用者可以單獨新增到這些群組中，但大量執行此操作需要額外的步驟。以下為可以完成此操作的一種方法：

* 在 Admin Console/IMS 中建立一或多個新群組，以存取集合/私人資料夾並將其設定為適用於 AEM。
* 以群組成員身分登入，以便在 AEM 中建立群組。
* 對於已移轉的集合或私人資料夾，使用資產使用者介面增加新群組作為編輯者/擁有者/檢視者。
* 將使用者新增 (或大量上傳) 到 Admin Console 中的新群組。
* 使用者首次登入時，便會在 AEM 中建立他們的 IMS 使用者，然後應該就能夠存取新群組，進而存取原始集合或私人資料夾群組。

注意事項：如要大量指派使用者，必須依照上述步驟於 IMS 中建立使用者；已存在於 IMS 的使用者無法透過大量上傳再次建立，但可以使用大量編輯器進行此類變更 (請參閱&#x200B;**編輯使用者詳細資料**&#x200B;下的 [Admin Console 大量使用者上傳](https://helpx.adobe.com/tw/enterprise/using/bulk-upload-users.html))。
