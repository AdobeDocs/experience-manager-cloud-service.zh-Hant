---
title: 移轉關閉的使用者群組
description: 瞭解將內容移轉至Adobe Experience Manager as a Cloud Service後啟用封閉使用者群組所需的特殊考量事項。
hide: true
hidefromtoc: true
exl-id: f62ed751-d5e2-4a01-8910-c844afab5733
feature: Migration
role: Admin
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 13%

---


# 移轉關閉的使用者群組 {#migrating-closed-user-groups}

>[!CONTEXTUALHELP]
>id="aemcloud_cug_migration"
>title="封閉使用者群組的移轉"
>abstract="封閉使用者群組 (CUG) 的移轉目前需要執行一些檢查和步驟，以便在移轉後正常運作。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html" text="AEM 中的封閉使用者群組"

目前，封閉使用者群組(CUG)需要一些額外的步驟，才能在移轉的目標環境中正常運作。 本檔案將說明相關情境，以及要求他們以預期方式保護節點所需的步驟。

## 封閉式使用者群組(CUG)的移轉

如果群組透過內容的ACL或其CUG原則節點與已移轉的內容相關聯，則會自動包含在CTT/CAM移轉至Adobe Experience Manager as a Cloud Service中。 驗證群組及其成員是否存在，應在上線前完成。 參照CUG原則的群組稱為「CUG群組」。

若要在AEM as a Cloud Service中使用CUG，使用者必須出現在製作例項上，並成為相關CUG群組的成員。  這可以使用套件完成，或者，如果CUG使用者是IMS使用者，則他們可能已存在。  接著，CUG使用者必須成為AEM CUG群組的成員。

若要啟用發佈執行個體上的CUG行為，

1. 必須啟動CUG群組（這會將它們及其成員複製到發佈執行個體），
1. 必須取消發佈受CUG原則保護的所有&#x200B;*頁面（以清除全域CUG計數），並且*
1. 接著，必須發佈受CUG原則保護的頁面（如此可讓發佈執行個體並追蹤原則）。
1. 發佈所有頁面後，請確認每個受CUG保護頁面的功能。

如需其他資訊，請參閱[已關閉的使用者群組](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/closed-user-groups.html)。
