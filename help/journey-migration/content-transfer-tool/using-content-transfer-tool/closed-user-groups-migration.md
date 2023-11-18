---
title: 移轉關閉的使用者群組
description: 瞭解將內容移轉至Adobe Experience Manager as a Cloud Service後啟用封閉使用者群組所需的特殊考量事項。
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 9%

---

# 移轉關閉的使用者群組 {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="封閉使用者群組移轉"
>abstract="封閉使用者群組 (CUG) 的移轉目前需要執行一些檢查和步驟，以便在移轉後正常運作。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html?lang=zh-Hant" text="AEM 中的封閉使用者群組"

目前，封閉使用者群組(CUG)需要一些額外的步驟，才能在移轉的目標環境中正常運作。 本檔案將說明相關情境，以及要求他們以預期方式保護節點所需的步驟。

## 群組移轉

如果主體（包括群組）透過該內容的ACL與移轉的內容相關聯，則會自動包含在移轉至Adobe Experience Manager as a Cloud Service中。

## 移轉中的封閉式使用者群組

目前，相關聯的群組 *僅限* 封閉使用者群組(CUG)原則為 *非* 自動包含在擷取中。 如上所述，如果透過ACL與任何內容相關聯，則會移轉這些使用者。 驗證群組及其成員是否存在，應在上線前完成。 透過「內嵌工作」檢視下載的「主體報表」可用來檢視相關群組是否包含，或因不在ACL中而不包含。 如果群組不存在，應在Author例項中建立該群組（包括新增適當成員），並啟動該群組，使其存在於Publish例項上。 您可以使用在來源上建立的封裝來完成此操作。

最後，必須觸發程式，且必須設定屬性以啟用CUG。 為此，請重新發佈與CUG原則相關的所有頁面。 這樣會校準Publish執行個體以追蹤原則。

這樣會啟用「發佈」上的CUG原則，而且只有屬於與原則相關群組成員的已驗證使用者才能存取內容。

## 使用中的開發

移轉團隊正致力於讓CUG原則自動移轉及運作，在擷取內容後無需任何其他步驟。
在嘗試上線之前，請將CUG功能包含在任何測試程式中。

## 摘要

總而言之，以下是移轉後啟用CUG的步驟：

1. 請確定CUG原則中使用的每個群組，在移轉後都存在於發佈上。
   - 如果移轉內容的ACL中包含群組，則群組可能存在。
   - 如果沒有，請使用套件將其安裝在目的地執行個體上（或在那裡手動建立），並啟動它及其成員。 然後確認它存在於Publish上。
1. 重新發佈與CUG原則相關聯的所有頁面，例如先編輯頁面，以確保發佈該頁面。 請務必將其全部重新發佈。
   - 重新發佈所有頁面後，請確認每個受CUG保護頁面的功能。
