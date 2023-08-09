---
title: 移轉封閉式使用者群組
description: 本頁提供將內容移轉至Adobe Experience Manager as a Cloud Service後啟用封閉使用者群組的必要特殊考量事項。
hide: true
hidefromtoc: true
source-git-commit: ca3c4bae2e652d75190d68c76b1dd4e09239f16c
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 0%

---

# 移轉封閉式使用者群組 {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="移轉封閉使用者群組"
>abstract="封閉使用者群組(CUG)的移轉目前需要一些檢查與步驟，才能在移轉後正常運作。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html" text="AEM中的封閉使用者群組"

目前，封閉使用者群組(CUG)需要一些額外的步驟，才能在移轉的目標環境中正常運作。  本檔案將說明相關情境，以及要求他們以預期方式保護節點所需的步驟。

## 群組移轉

如果主體（包括群組）透過該內容的ACL與移轉的內容相關聯，則會自動包含在移轉至Adobe Experience Manager as a Cloud Service中。

## 移轉中的封閉式使用者群組

目前，相關聯的群組 *僅限* 封閉使用者群組(CUG)原則為 *非* 自動包含在擷取中。 如果它們透過ACL與任何內容相關聯（如上所述），則會遷移。 該群組存在的驗證應在上線前完成。 透過「內嵌工作」檢視下載的「主體報表」可用來檢視相關群組是否包含，或因不在ACL中而不包含。 如果群組不存在，應在Author例項中建立該群組（包括新增適當成員），並啟動該群組，使其存在於Publish例項上。

最後，必須觸發程式才能啟用CUG。 若要這麼做，請重新發佈任何包含CUG原則的內容。 因此，在正常測試程式中，如果發現CUG無法運作，請重新發佈該內容（即使未修改亦會發佈）。

這應該會在發佈上啟用CUG原則，而且只有與原則相關聯之群組成員的已驗證使用者才能存取內容。

## 使用中的開發

移轉團隊正致力於讓CUG原則自動移轉及運作，在擷取內容後無需執行任何其他步驟。
在嘗試上線之前，建議在任何測試程式中包含CUG功能。

## 摘要

總而言之，以下是移轉後啟用CUG的步驟：

1. 請確定CUG原則中使用的每個群組，在移轉後都存在於發佈上。
   - 如果移轉內容的ACL中包含群組，則群組可能已存在。
   - 如果沒有，請使用套件在目的地執行個體上安裝它（或在那裡手動建立），並啟動它及其成員。 然後確認它存在於Publish上。
1. 如果CUG原則尚未保護節點，請再次重新發佈頁面（即使未對該頁面進行任何變更，也會確保該頁面已發佈）。
   - 驗證每個受CUG保護的節點。
